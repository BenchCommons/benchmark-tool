# AGENTS.md — tools-benchmark

Follow the org-wide rules in [BenchCommons/.github AGENTS.md](https://github.com/BenchCommons/.github/blob/main/AGENTS.md) and the decisions in [.product](https://github.com/BenchCommons/.product). This file only adds what is specific to this repo.

## Role
Tool: builds each catalog implementation in Docker, runs it and records reproducible results. It is derived from the TechEmpower toolset. It owns the **catalog contract** and the **published results format** (see `.product/CONTRACTS.md`).

## Stack and commands
- Python 3.12. `./ssgberk` builds the toolset image and runs `toolset/run-tests.py`.
- `frameworks/` is a submodule pointing to `BenchCommons/catalog-ssg`.
- Results are written to `results/<ts>/results.json` and published under `docs/results/<date>/<suite>/<cell>/`.
- Checks: ruff (py312), pytest, compileall, docker build.
- Specs and their order: `docs/specs/` (see `ROADMAP.md`).

## Rules
- Generalizing beyond SSGs (tools-benchmark#29) and switching to perfratio (#30) are tracked in issues. Do not hard-code new SSG-only assumptions.
