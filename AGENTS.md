# SIN-Code-EFM-Tool — Ephemeral Full-Stack Mocking — spin up disposable test environments (FastAPI + uvicorn + pydantic) with Docker/OrbStack support for reproducible integration tests.

<!--
  Docs: this file follows the SIN-Code AGENTS.md standard
  (see OpenSIN-Code/SIN-Code AGENTS.md section "Ecosystem map" and
  issue #40). sin-brain discovers rules via the section headers below;
  sin-context-bridge queries this file via the "## Architecture" anchor.
  Generated: 2026-06-13; standard version: v1 (chore/issue-40).
-->

## Architecture

Orchestration layer that builds, runs, and tears down ephemeral test stacks (FastAPI app + uvicorn + pydantic models + optional Docker containers). Two runtimes supported: Docker (Linux CI) and OrbStack (macOS dev). Main entry point: `sin_code_efsm.cli:app` (Typer). Consumed by integration tests and the `sin efm` HubTool.

## Services

| Service | Port | Purpose |
| ------- | ---- | ------- |
| CLI     | N/A  | `efsm <subcommand>` — up, down, list, status |
| Docker/OrbStack | dynamic | ephemeral stacks can expose arbitrary ports |

## Quick-Start

```bash
pip install -e .[docker]
efsm --help
efsm up my-stack.yaml --ttl 3600
efsm list
efsm down <stack-id>
```

## Key Endpoints / Commands

- `efsm up` — spin up an ephemeral test stack from YAML config
- `efsm down` — tear down a running stack
- `efsm list` — list all running ephemeral stacks
- `efsm status` — show status of a specific stack

## CoDocs

- All Python source files in `src/sin_code_efm/` MUST have a `.doc.md` companion.
- Run `sin codocs check` to validate. Output MUST be `OK: ≥5 files` to pass.
- CoDocs companion for THIS file: none (AGENTS.md is itself a doc).

## Testing

```bash
pytest tests/ -v
pytest tests/test_agents_md.py -v
```

Expected: 10 tests pass (9 existing + 1 from issue #40).

## Integration

- **sin-code HubTool:** `sin code efm <action>` (e.g. `sin code efm up`).
- **MCP server:** `efm` exposes MCP via the `sin-code serve` adapter; the
  tool prefix in MCP namespace is `efm__*` (e.g. `efm__up`).
- **Cross-repo:** called by `sin code full` and the integration-test suite in SIN-Code/AGENTS.md. On macOS, default runtime is OrbStack (`orb`); on Linux CI, Docker. Auto-detected via `uname`.

---

<!-- gitnexus:start -->
# GitNexus — Code Intelligence

This project is indexed by GitNexus as **SIN-Code-EFM-Tool** (140 symbols, 207 relationships, 1 execution flows). Use the GitNexus MCP tools to understand code, assess impact, and navigate safely.

> If any GitNexus tool warns the index is stale, run `npx gitnexus analyze` in terminal first.

## Always Do

- **MUST run impact analysis before editing any symbol.** Before modifying a function, class, or method, run `gitnexus_impact({target: "symbolName", direction: "upstream"})` and report the blast radius (direct callers, affected processes, risk level) to the user.
- **MUST run `gitnexus_detect_changes()` before committing** to verify your changes only affect expected symbols and execution flows.
- **MUST warn the user** if impact analysis returns HIGH or CRITICAL risk before proceeding with edits.
- When exploring unfamiliar code, use `gitnexus_query({query: "concept"})` to find execution flows instead of grepping. It returns process-grouped results ranked by relevance.
- When you need full context on a specific symbol — callers, callees, which execution flows it participates in — use `gitnexus_context({name: "symbolName"})`.

## Never Do

- NEVER edit a function, class, or method without first running `gitnexus_impact` on it.
- NEVER ignore HIGH or CRITICAL risk warnings from impact analysis.
- NEVER rename symbols with find-and-replace — use `gitnexus_rename` which understands the call graph.
- NEVER commit changes without running `gitnexus_detect_changes()` to check affected scope.

## Resources

| Resource | Use for |
|----------|---------|
| `gitnexus://repo/SIN-Code-EFM-Tool/context` | Codebase overview, check index freshness |
| `gitnexus://repo/SIN-Code-EFM-Tool/clusters` | All functional areas |
| `gitnexus://repo/SIN-Code-EFM-Tool/processes` | All execution flows |
| `gitnexus://repo/SIN-Code-EFM-Tool/process/{name}` | Step-by-step execution trace |

## CLI

| Task | Read this skill file |
|------|---------------------|
| Understand architecture / "How does X work?" | `.claude/skills/gitnexus/gitnexus-exploring/SKILL.md` |
| Blast radius / "What breaks if I change X?" | `.claude/skills/gitnexus/gitnexus-impact-analysis/SKILL.md` |
| Trace bugs / "Why is X failing?" | `.claude/skills/gitnexus/gitnexus-debugging/SKILL.md` |
| Rename / extract / split / refactor | `.claude/skills/gitnexus/gitnexus-refactoring/SKILL.md` |
| Tools, resources, schema reference | `.claude/skills/gitnexus/gitnexus-guide/SKILL.md` |
| Index, status, clean, wiki CLI commands | `.claude/skills/gitnexus/gitnexus-cli/SKILL.md` |

<!-- gitnexus:end -->
