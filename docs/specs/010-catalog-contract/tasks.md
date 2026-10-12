# 010 Catalog Contract: Tasks

Read `spec.md` and `plan.md` (Global Constraints, Contracts, Decisions, Review Focus) first. Every task's requirements include the Global Constraints. Run commands from the repository root. Commit with `git commit -S` as configured; never pass `--no-gpg-sign` or `--author`. End every commit message with:

```
Co-Authored-By: Claude Opus 5.5 (1M context) <noreply@anthropic.com>
```

Test command (no Docker): `python3 -m pytest -q` and `ruff check toolset tests tools`.

Each task is one PR with green CI. Tasks 1 to 3 are independent; 4 needs 1; 5 needs 3 and 4; 6 needs 4; 7 needs 4.

---

### Task 1: Schemas and the stdlib validator

**Files:**
- Create: `schema/catalog.schema.json`, `schema/benchmark_config.schema.json`, `schema/implementation.base.schema.json`, `toolset/utils/jsonschema_lite.py`
- Test: `tests/test_schemas.py`

**Interfaces:**
- Produces: `jsonschema_lite.validate(instance, schema) -> list[str]` (empty when valid; each item `"<json pointer>: <message>"`).

- [ ] **Step 1:** Write failing tests: the CS manifest from `plan.md` validates; a manifest with `contractVersion: "1"`, a missing `implementations` or an unknown test type fails with a pointer to the field; `tests/fixtures/generators.json` entries plus a `version` validate against the base schema; CS `Go/hugo/benchmark_config.json` (copied to `tests/fixtures/catalogs/ssg/Go/hugo/`) validates; the `algorithm` and `http` examples from `plan.md` validate; an entry with `test_type: "algorithm"` and no `run_command` fails.
- [ ] **Step 2:** Implement the validator subset listed in `plan.md` (Tech stack) and the three schemas. `implementation.base.schema.json` leaves `additionalProperties` open so catalog schemas can extend it with `allOf`.
- [ ] **Step 3:** `python3 -m pytest -q tests/test_schemas.py`, ruff, commit `feat(schema): catalog contract schemas (spec 010 R-1, R-8, R-10)`.

### Task 2: `tools/check_catalog.py`

**Files:**
- Create: `tools/check_catalog.py`, `tests/test_check_catalog.py`, `tests/fixtures/catalogs/ssg/**` (`catalog.json`, `generators.json`, `schema/generator.schema.json`, `Go/hugo/{hugo.dockerfile,build.sh,benchmark_config.json,generator.json}`, `Go/zola/…`), `tests/fixtures/catalogs/algorithms/**` (two implementations of one algorithm)
- Modify: `.github/workflows/ci.yml` (job `catalog-ssg-contract`: check out `BenchCommons/catalog-ssg` default branch, write the CS manifest from `plan.md` into it, run the checker)

**Interfaces:**
- Consumes: Task 1 schemas (loaded from `schema/` relative to the script).
- Produces: CLI `python3 tools/check_catalog.py <catalog-dir> [--skip-index-check]`; exit 0 when clean, 1 with one `<path>: <rule>: <message>` line per violation. Rules are named `manifest`, `files`, `runner`, `dockerfile`, `config`, `metadata`, `ids`, `index` (R-20).

- [ ] **Step 1:** Write failing tests, one fixture per rule: missing `catalog.json`; implementation without its Dockerfile; runner copy differing by one byte; `FROM ubuntu` (no tag) and `FROM node:latest`; a download without an `ARG *_VERSION`; an invalid `benchmark_config.json`; metadata `id` differing from the directory name (and, for the algorithms layout, from the index entry); a duplicated id; `index.check` exiting 1. Plus: both clean fixtures exit 0.
- [ ] **Step 2:** Implement. `dockerfile` rule: every `FROM` has an explicit tag other than `latest` (or a digest); every `curl`/`wget` URL that contains a version-like segment uses `${…_VERSION}`. `index` rule runs `index.check` with `cwd=<catalog-dir>` and a 300 s timeout.
- [ ] **Step 3:** Add the CI job (Review Focus 4). Tests, ruff, commit `feat(tools): catalog conformance checker (spec 010 R-20)`.

### Task 3: Generic markers with `SSGBERK_*` aliases

**Files:**
- Modify: `toolset/utils/results.py`
- Test: `tests/test_results.py` (append)

**Interfaces:**
- Produces: `results.normalize_markers(raw: str) -> tuple[str, str]` returning `(text, marker_prefix)`; `parse_build_output` calls it first and adds `markerPrefix`, `engine`, `engineVersion` to every result dict. Constants move to `BENCH_*` names; `PROFILE_UNSUPPORTED` becomes `BENCH_UNSUPPORTED`.

- [ ] **Step 1:** Write failing tests:
  - each of `raw_ok.txt`, `raw_v2_ok.txt`, `raw_conformance_fail.txt`, `raw_unsupported.txt` parses to the same dicts as on `master`, plus `markerPrefix: "SSGBERK"`, `engine: "hyperfine"`, `engineVersion: null` (goal 2);
  - the same fixtures with `SSGBERK_` replaced by `BENCH_` give the same dicts with `markerPrefix: "BENCH"`;
  - `BENCH_RESULT_BEGIN engine=perfratio version=1.3.0` sets `engine` and `engineVersion`;
  - `test_alias_inside_json_untouched`: a hyperfine `command` string containing `SSGBERK_GENERATE_ONLY` keeps it verbatim (Review Focus 1).
- [ ] **Step 2:** Implement with the normalization in `plan.md` (Markers). Every existing regex keeps `_BOL`.
- [ ] **Step 3:** Tests, ruff, commit `feat(results): generic BENCH_ markers, SSGBERK_ aliases (spec 010 R-15, R-16)`.

### Task 4: Catalog selection and discovery

**Files:**
- Create: `toolset/utils/catalog.py`, `tests/test_catalog.py`
- Modify: `toolset/run-tests.py` (`--catalog`, `--catalog-dir`), `toolset/utils/benchmark_config.py` (`lang_root` → `catalog.root`), `toolset/utils/metadata.py` (discovery by `catalog.implementations`; language from metadata), `toolset/utils/audit.py`, `toolset/utils/scaffolding.py`, `toolset/github_actions/github_actions_diff.py`

**Interfaces:**
- Produces: `catalog.load(fw_root: str, name: str | None, directory: str | None) -> Catalog`; `Catalog` has `name`, `root`, `contract_version`, `test_types`, `runner_file`, `metadata_file`, `index_path`, `index_key`, `implementation_dirs() -> list[str]`, `index_entry(id) -> dict | None`, `commit() -> str | None`. `SUPPORTED_CONTRACT = (1, 1)`.

- [ ] **Step 1:** Write failing tests:
  - no flags and no `catalog.json` in `frameworks/` → built-in CS manifest, root `frameworks/`;
  - `--catalog ssg` with `catalogs/ssg/catalog.json` present → that manifest;
  - `--catalog-dir tests/fixtures/catalogs/algorithms` → algorithms manifest;
  - `contractVersion: 2` → error naming `2` and the supported range (R-2);
  - `test_gather_tests_algorithms_layout`: `metadata.gather_tests` finds both fixture implementations and `--test-lang Python` filters by the metadata `language` (Review Focus 3);
  - status `removed` in the index is skipped unless named with `--test` (R-11).
- [ ] **Step 2:** Implement; then `grep -rn "frameworks" toolset` per Review Focus 2.
- [ ] **Step 3:** Existing suite passes unchanged (`python3 -m pytest -q`). Commit `feat(toolset): select a catalog with --catalog/--catalog-dir (spec 010 R-17)`.

### Task 5: `algorithm` test type, `http` declaration, suites per catalog

**Files:**
- Create: `toolset/benchmark/test_types/algorithm_type.py`, `toolset/benchmark/test_types/http_type.py`, `tests/test_algorithm_type.py`, `tests/fixtures/raw_algorithm_ok.txt`, `tests/fixtures/raw_algorithm_verify_fail.txt`, `tests/fixtures/raw_algorithm_unsupported.txt`
- Modify: `toolset/benchmark/test_types/__init__.py`, `toolset/benchmark/suites.py`, `toolset/benchmark/suites.json` (add `algo-smoke` from `plan.md`), `toolset/utils/docker_helper.py` (pass the runner environment from `plan.md`)

**Interfaces:**
- Produces: each test type class exposes `PARAMETERS` (cell keys with types), `CONFIG_KEYS`, `env(cell) -> dict[str, str]` and `parse(raw) -> list[dict]`. `DataRateType.env` returns both `BENCH_*` and legacy names. `HttpType` raises `NotImplementedError("http: see spec 010, Out of scope")` from `env` and `parse`.

- [ ] **Step 1:** Write failing tests:
  - `DataRateType.env({"numberOfFiles": 100, "contentSize": "0.500"})` contains `number_of_files=100`, `BENCH_NUMBER_OF_FILES=100`, `content_size=0.500`, `BENCH_CONTENT_SIZE=0.500`;
  - `AlgorithmType.parse` of the three fixtures gives one result with `algorithm`, `n` and the timing keys; `failed` with reason `verify: BENCH_VERIFY_FAIL sha256 …`; `unsupported` (goal 3);
  - `suites.load` accepts `algo-smoke`, rejects a cell with `numberOfFiles` in an `algorithm` suite, and defaults old suites to `ssg`/`datarate`;
  - `--suite algo-smoke` with `--catalog ssg` is refused (R-18);
  - selecting a catalog whose `testTypes` is `["http"]` exits with the `NotImplementedError` message, not a traceback.
- [ ] **Step 2:** Implement.
- [ ] **Step 3:** Tests, ruff, commit `feat(test-types): algorithm test type and per-catalog suites (spec 010 R-12–R-14, R-18)`.

### Task 6: `catalog` in `results.json`

**Files:**
- Modify: `toolset/utils/results.py`, `toolset/utils/merge_results.py`
- Test: `tests/test_results.py`, `tests/test_merge_results.py` (append)

- [ ] **Step 1:** Write failing tests: a run writes `catalog: {"name", "commit", "contractVersion"}`; `--parse` of an old run without it keeps it absent; `merge()` of two `ssg` inputs keeps `catalog`; `merge()` of `ssg` and `algorithms` inputs raises with both names (Decision 5); `schemaVersion` stays `2`.
- [ ] **Step 2:** Implement. Commit `feat(results): record the catalog (spec 010 R-19)`.

### Task 7: Submodule, README, CONTRACTS link

**Files:**
- Modify: `.gitmodules` (add `catalogs/ssg` → `https://github.com/BenchCommons/catalog-ssg`, same commit as `frameworks/`), `README.md` (catalog selection, link to this spec as the contract), `ssgberk` (no flag change; document `--catalog-dir`)

- [ ] **Step 1:** `git submodule add https://github.com/BenchCommons/catalog-ssg catalogs/ssg` and check out the commit `frameworks/` points at.
- [ ] **Step 2:** README section "Catalogs" with the `catalog.json` example and the marker table from `spec.md`.
- [ ] **Step 3:** Commit `chore: add catalogs/ssg submodule and document catalogs (spec 010)`. After merge, open a PR in `BenchCommons/.product` changing the `CONTRACTS.md` catalog row's status to `docs/specs/010-catalog-contract` (goal 5), and comment on CS #203, CA #11 and CW #1 with the link.
