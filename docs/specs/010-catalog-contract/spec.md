# 010 Catalog Contract

- **Date:** 2026-10-12
- **Status:** proposed, awaiting review
- **Repo:** `BenchCommons/benchmark-tool` (BT). This repo owns the contract; catalogs reference it and never redefine it (`.product` `CONTRACTS.md`).
- **Issue:** #29
- **Consumers:** `BenchCommons/catalog-ssg` (CS), `BenchCommons/catalog-algorithms` (CA), `BenchCommons/catalog-web-frameworks` (CW).
- **Related:** BT #30 and `perfratio#240` (measurement engine and its output schema, owned by perfratio), `dataset-tool#1` (input datasets), `catalog-algorithms#11` (tracking), `.product` ADR 0001 (naming) and ADR 0004 (TechEmpower continuation), BT 002 (markers, toolset side), BT 008 (suites, `results.json` v2), CS 001 (canonical `build.sh`), CS 004 (`generator.json`, `generators.json`).

## Context

BT measures one catalog, and assumes SSG semantics everywhere:

| Item | Today | Problem for other catalogs |
|---|---|---|
| Catalog source | one submodule, `frameworks/` → `ssg-frameworks` (now CS) | no way to point at CA or CW |
| Layout | `<Lang>/<id>/` with `<id>.dockerfile`, `build.sh`, `benchmark_config.json`, `generator.json` | CA uses `languages/<lang>/<algorithm>/` (CA spec 011); CW inherits TechEmpower's `frameworks/<Lang>/<id>/` |
| Runner | `build.sh`, byte-identical in every generator, checked by CS `tools/check-build-sh.sh` | the rule is only written down in CS |
| Metadata | `generator.json` + `schema/generator.schema.json`; index `generators.json` built by CS `tools/build_index.py --check` | CA has `meta.json`; no shared base fields |
| Test type | only `datarate` (`numberOfFiles`, `contentSize`) | CA needs input size `n`; CW needs HTTP endpoints |
| Correctness | `SSGBERK_VERIFY_OK/FAIL` (output file count) and `SSGBERK_CONFORMANCE_*`, untimed, before `STARTTIME` (BT 008 R-15) | named after one catalog; HTTP needs the toolset to verify, as TechEmpower's verify stage did |
| Result | hyperfine JSON between `SSGBERK_RESULT_BEGIN/END`, into `results.json` `schemaVersion: 2` `rawData.datarate.<id>` | marker names; engine fixed to hyperfine |

TechEmpower solved the same problem for web frameworks: a per-implementation `benchmark_config.json` with one entry per test, a Dockerfile per test, and a verify stage that checks every endpoint before any load is applied. BT is derived from that toolset. This spec keeps that shape and writes down, once, what every catalog must provide and what BT does with it.

## Terms

- **Catalog:** a repo of implementations measured by BT (`catalog-*`, ADR 0001).
- **Implementation:** one directory in a catalog that BT builds into one image and measures. Its **id** is unique within the catalog.
- **Test type:** what is measured and how it is checked: `datarate`, `algorithm`, `http`. A test type defines its parameters, its verification and its result shape.
- **Cell:** one combination of test type parameters (e.g. `numberOfFiles=1000, contentSize=500`, or `algorithm=nbody, n=5000000`).
- **Engine:** the program that times the runs inside the container: hyperfine today, perfratio after BT #30.

## Requirements

### Catalog manifest

- **R-1** A catalog has `catalog.json` at its root, valid against BT `schema/catalog.schema.json`. Fields:
  - `contractVersion` (integer, this spec defines `1`);
  - `name` (`ssg`, `algorithms`, `web-frameworks`);
  - `testTypes`: the test types the catalog uses, from R-12;
  - `implementations`: a glob, relative to the root, that matches every implementation directory (`*/*` for CS, `languages/*/*` for CA, `frameworks/*/*` for CW);
  - `runner`: `{ "file": "<name>", "canonical": "<path>" }`, the per-implementation runner file name and the reference copy (CS: `build.sh`, `Go/hugo/build.sh`). `file` is omitted for `http`-only catalogs (R-6);
  - `metadata`: `{ "file": "<name>", "schema": "<path>" }` (CS: `generator.json`, `schema/generator.schema.json`);
  - `index`: `{ "file": "<path>", "key": "<array key>", "check": "<command>" }` (CS: `generators.json`, `generators`, `python3 tools/build_index.py --check`).
- **R-2** BT supports a closed range of `contractVersion` values and refuses a catalog outside it, with an error that names both versions. The range starts at `[1, 1]`.

### Implementation directory

- **R-3** Every directory matched by `implementations` contains:
  - `<id>.dockerfile` (R-4);
  - `benchmark_config.json` (R-8);
  - the metadata file (R-10);
  - the runner file, unless the catalog is `http`-only (R-5, R-6);
  - `src/` or other inputs the Dockerfile copies. No file outside the directory is read at build time; the build context is the directory.

  `<id>` is the directory name. It matches `^[a-z0-9][a-z0-9._-]*$` and is unique in the catalog. In CA's `languages/<lang>/<algorithm>/` the leaf name repeats across languages (every language has `hello-world`), so CA's id is `<lang>.<algorithm>` (e.g. `python.hello-world`) through the metadata `id` field; R-11 checks it equals the parent and leaf directory names joined by a dot.
- **R-4** The Dockerfile is **pinned**:
  - the base image names an exact tag (`ubuntu:24.04`, `node:24.11.0-bookworm-slim`), never `latest` or a bare name; a digest (`@sha256:`) is recommended and, when absent, BT records the resolved digest in `results.json` (BT 008, unchanged);
  - every downloaded tool, toolchain and engine is installed at an exact version, set by an `ARG <NAME>_VERSION=` line (CS `hugo.dockerfile`: `HYPERFINE_VERSION`, `HUGO_VERSION`);
  - package-manager installs use a lockfile or exact versions;
  - the engine (hyperfine 1.20.0 today; perfratio after BT #30) is installed in the image, so timing happens inside the container and never wraps `docker run`;
  - the image works on `linux/amd64` and `linux/arm64`, or the metadata says which one it supports (R-10 `platforms`).

### Runner

- **R-5** The runner is the only entry point BT calls in a measured container. Every implementation in a catalog carries a **byte-identical** copy of `runner.canonical`; implementation-specific behaviour comes from `benchmark_config.json`, never from editing the runner. The check is the one CS already runs (`cmp` against the canonical copy, `tools/check-build-sh.sh`), generalized in R-20.
- **R-6** `http` implementations have no runner: the image's `CMD` starts the server and BT drives it from outside (R-15). This is the TechEmpower model and the only exception to R-5.
- **R-7** The runner reads its inputs from environment variables set by BT (names in `plan.md`, Contracts): the generic `BENCH_TEST_TYPE`, `BENCH_RUNS`, `BENCH_WARMUP`, `BENCH_VERBOSE`, plus the cell parameters of its test type (R-12). For compatibility, `datarate` also receives today's names (`number_of_files`, `content_size`, `min_runs`, `verbose_build`).

### Metadata

- **R-8** `benchmark_config.json` keeps the TechEmpower shape that BT already reads (`toolset/utils/metadata.py`): top-level `framework` (= id) and `tests`, a list of one-key objects `{ "<testName>": { ... } }` with `default` required. Each test entry carries:
  - the display fields BT already validates (`approach`, `classification`, `framework`, `language`, `display_name`, `notes`, `versus`);
  - `test_type` (from the catalog's `testTypes`; absent means `datarate`, for compatibility);
  - the test-type keys from R-12.

  CS's top-level `content` and `config` lists stay valid as `datarate` keys (R-12).
- **R-9** BT publishes `schema/benchmark_config.schema.json` and validates every `benchmark_config.json` on load. An invalid file is reported with its path and skipped, not a crash.
- **R-10** The metadata file describes the implementation for people and the website; BT reads only the base fields. BT publishes `schema/implementation.base.schema.json` with the base fields: `id`, `name`, `language`, `version` (string, the measured version), `license`, `homepage`, `repository`, `benchmark.status` (`active`, `wip`, `removed`), optional `platforms` (`["linux/amd64", "linux/arm64"]` by default). A catalog's metadata schema references the base with `allOf` and adds its own fields (CS: `templateEngines`, `contentFormats`, …). CS `generator.json` already has every base field except `version`, which CS writes into `generators.json`; R-11 accepts the version from either place.
- **R-11** The catalog index (`index.file`) lists every implementation: `schemaVersion`, `generatedFrom` (catalog commit) and, under `index.key`, one entry per implementation with at least `id`, `path` (relative to the root), `version` and `benchmark.status`. It is generated by the catalog's own tool, and `index.check` exits non-zero when the index is stale or invalid (CS `build_index.py --check` already does this). BT reads versions from the index (as BT 008 does with `generators.json`) and skips implementations whose status is not `active` unless named with `--test`.

### Test types

- **R-12** A test type is a BT plug-in under `toolset/benchmark/test_types/` that declares its cell parameters, the `benchmark_config.json` keys it reads, its verification and its result shape. This spec defines three:

  | Test type | Catalog | Cell parameters | Config keys | Verification (untimed, before any timed run) | Timed work |
  |---|---|---|---|---|---|
  | `datarate` | CS | `numberOfFiles`, `contentSize` | `content[]`, `config[]` (`build_command`, `output_folder`, `output_glob`, `cache_folders`, …) | one build; runner prints `VERIFY_OK` when the output count equals `numberOfFiles`, plus `CONFORMANCE_*` (CS 006) | cold full rebuild per run (BT 008 R-15) |
  | `algorithm` | CA | `algorithm` (id), `n` (input size), optional `dataset` (`<name>@<version>`, dataset-tool#1) | `run_command`, optional `build_command` (compile step, untimed) | one run with the cell's input; runner prints `VERIFY_OK` when the SHA-256 of stdout equals the expected checksum for `(algorithm, n)` from the catalog's algorithm definition (CA 010) | the run command with the same input |
  | `http` | CW | `endpoint` (`json`, `plaintext`, `db`, `query`, `fortune`, `update`, `cached-query`), `concurrency`, `durationSeconds` | `port`, `<endpoint>_url` per endpoint (TechEmpower keys) | BT requests each URL and applies TechEmpower's verifier rules (status, headers, body); `VERIFY_OK/FAIL` are written by BT | load generator in a separate container, after a warmup |

- **R-13** The verification is mandatory and untimed. A cell is timed only after `VERIFY_OK` (and, where the test type has one, `CONFORMANCE_OK` subject to `--require-conformance`, BT 008 decision 5). A missing or failed verification gives status `failed` with reason `verify: <first FAIL line>` or `protocol: verification markers missing before STARTTIME` (BT 008 R-15, unchanged).
- **R-14** A test type may declare that an implementation does not support a cell (e.g. an algorithm not implemented in that language, a profile not supported). The runner prints `UNSUPPORTED <reason>` and exits 3; BT records `unsupported.<testType>` (BT 008 R-7, generalized).

### Result markers

- **R-15** The process that times the work writes the markers to stdout: the runner for `datarate` and `algorithm`; BT's load-generator step for `http`. Markers start at the beginning of a line. The generic set, in order:

  ```
  BENCH_INPUT files=<n> bytes=<n>                (optional)
  BENCH_VERIFY_OK <details> | BENCH_VERIFY_FAIL <reason>
  BENCH_CONFORMANCE_OK|FAIL|PENDING <details>    (optional, test-type defined)
  BENCH_OUTPUT files=<n> bytes=<n>               (optional)
  BENCH_UNSUPPORTED <reason>                     (instead of everything after it; exit 3)
  STARTTIME <epoch>
  BENCH_RESULT_BEGIN engine=<name> version=<v>
  <engine JSON>
  BENCH_RESULT_END
  ENDTIME <epoch>
  ```

  `engine=` and `version=` are optional; absent means `hyperfine`. The JSON between the result markers is the engine's export, unchanged (hyperfine `--export-json`; perfratio's versioned schema from perfratio#240).
- **R-16** **Compatibility:** every `SSGBERK_<X>` marker is accepted as an alias of `BENCH_<X>`, and `SSGBERK_PROFILE_UNSUPPORTED` as an alias of `BENCH_UNSUPPORTED`. The parser normalizes both prefixes before applying BT 002 and BT 008 rules, so CS output today parses to the same result as before. Each result records `markerPrefix` (`BENCH` or `SSGBERK`) so the alias's use can be measured before it is removed. Removing the aliases needs a new `contractVersion`.

### Toolset

- **R-17** BT runs one catalog per run, chosen by `--catalog <name>` (default `ssg`) from submodules under `catalogs/<name>/`, or by `--catalog-dir <path>` for a local checkout. `--test`, `--exclude`, `--list-tests` and the suite options work on the selected catalog.
- **R-18** `toolset/benchmark/suites.json` entries gain `catalog` and `testType`, defaulting to `ssg` and `datarate`, and their cells hold the test type's parameters. Existing suites (`smoke`, `standard`, `stress`, `legacy-2019`, `P`, `M`, `G`, `GG`) are unchanged and keep their versions. `--suite` refuses a suite whose `catalog` differs from the selected one.
- **R-19** `results.json` stays `schemaVersion: 2` with one additive key, `catalog: {"name", "commit", "contractVersion"}`, and per-result `markerPrefix` (R-16). `rawData`, `succeeded`, `failed` and `unsupported` are already keyed by test type, so `algorithm` and `http` results go under their own keys. Engine fields (energy, custom metrics) and `schemaVersion: 3` belong to BT #30.
- **R-20** BT ships `tools/check_catalog.py <catalog-dir>` (stdlib only), which a catalog's CI runs against a pinned BT tag. It checks R-1 to R-11: manifest valid, every implementation has its files, runner copies are byte-identical, Dockerfiles have no unpinned base image or `latest`, every `benchmark_config.json` and metadata file validates, ids are unique and match the index, and `index.check` passes. It exits non-zero with one line per violation.

## Goals and success criteria

1. **CS conforms with only a manifest.** *Measured by:* with a `catalog.json` added to a CS checkout and no other change, `tools/check_catalog.py` exits 0, and `./ssgberk --test hugo -nf 50 -cs 5` produces a `results.json` whose `rawData`, `succeeded`, `failed` and rankings equal those of the same run before this spec (fixture comparison of `parse_build_output`).
2. **Aliases are equivalent.** *Measured by:* a unit test parses each existing `tests/fixtures/raw_*.txt` fixture as is and with `SSGBERK_` replaced by `BENCH_`; both give the same result except `markerPrefix`.
3. **A second catalog runs end to end.** *Measured by:* a fixture catalog in `tests/fixtures/catalogs/algorithms/` (two implementations, one algorithm, two values of `n`) passes `check_catalog.py`, and a unit test drives `algorithm` parsing from recorded runner output into `rawData.algorithm.<id>`, including one `VERIFY_FAIL` (checksum mismatch) recorded as `failed` and one `UNSUPPORTED` recorded under `unsupported.algorithm`.
4. **Violations are caught.** *Measured by:* `check_catalog.py` unit tests, one per rule in R-20, each on a fixture with exactly that violation.
5. **Contract is referenced, not copied.** *Measured by:* CS, CA and CW each have an issue linking to this spec (CS #203, CA #11, CW #1), and `.product` `CONTRACTS.md` changes the row's status from "to specify" to this spec's path.

## Out of scope

- The perfratio switch, its JSON parsing and `results.json` `schemaVersion: 3` (BT #30, perfratio#240).
- Renames: the `ssgberk` wrapper and image names, `SSGBERK_HOST_*` launcher variables, docs (issue #29, rename checkbox; separate spec).
- The `http` load generator and verifier implementation (forking TFBVerifier, ADR 0004): this spec fixes only the `http` test type's interface. Its BT implementation is a separate spec after CW 001.
- CA's algorithm set, reference inputs and expected checksums (CA 010) and the dataset input contract (dataset-tool#1).
- Changes inside any catalog; each catalog adopts the contract in its own spec.
- Running several catalogs in one invocation, and cross-catalog rankings.
- The website and published results layout (website#5).

## Migration and compatibility

| Step | Where | Change | Breaks anything? |
|---|---|---|---|
| 1 | BT | Schemas, `check_catalog.py`, alias-tolerant parser, `catalog` key in `results.json` | No. With no `catalog.json`, BT treats `frameworks/` as `ssg` with the manifest in `plan.md` (built-in default). |
| 2 | BT | `catalogs/ssg` submodule pointing at `BenchCommons/catalog-ssg`; `frameworks/` stays a submodule at the same commit until step 5 | No. `--catalog-dir frameworks` still works. |
| 3 | CS | Add `catalog.json`, add `version` to `generator.json` or keep it in the index (R-10), run `check_catalog.py` in CI (CS #203) | No. Runner, markers and layout unchanged. |
| 4 | CS | `build.sh` prints `BENCH_*` instead of `SSGBERK_*` (one PR, canonical copy and all copies) | No. BT accepts both (R-16). |
| 5 | BT | Remove `frameworks/` and the built-in default manifest once CS has `catalog.json` on its default branch | Local scripts that mount `frameworks/` must use `--catalog ssg`. |
| 6 | CA, CW | Adopt the contract in their own specs (CA 011–013, CW 001) | — |

The `SSGBERK_*` aliases stay for all of `contractVersion: 1`. `results.json` readers need no change: the new keys are optional (BT 008 R-28).
