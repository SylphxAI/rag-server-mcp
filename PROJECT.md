# RAG Server MCP

RAG Server MCP is a deprecated predecessor to CodeRAG. Its family role is
historical migration guidance only.

## Lifecycle

- State: `deprecated`
- Layer: `legacy`
- Successor: [`SylphxAI/coderag`](https://github.com/SylphxAI/coderag)

## Goals

- Keep migration guidance clear for any remaining users.
- Avoid new implementation work that competes with CodeRAG.
- Preserve historical context without becoming an active package surface.

## Non-Goals

- This repository does not own current code retrieval, code indexing, vector
  search, MCP package release, or benchmark strategy.
- This repository does not own future architecture intelligence work.
- This repository should not publish new feature versions.

## Public Surfaces

- Migration README: [`README.md`](README.md)
- Package manifest: [`package.json`](package.json)
- SOTA family roadmap: [`docs/roadmap/sota-family-roadmap.md`](docs/roadmap/sota-family-roadmap.md)
