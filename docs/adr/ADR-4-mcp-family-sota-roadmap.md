# ADR-4: Adopt RAG Server MCP Retirement Roadmap

Date: 2026-07-09
Status: Proposed in PR #4
Slug: mcp-family-sota-roadmap

## Context

RAG Server MCP is the deprecated predecessor to CodeRAG. It needs a repo-local
roadmap that makes retirement explicit and prevents future work from splitting
code-retrieval ownership.

## Decision

Adopt `docs/roadmap/sota-family-roadmap.md` as the repo-local retirement
roadmap.

Future code retrieval work belongs in CodeRAG. This repository remains
deprecated and should publish only emergency security forward fixes if needed.

## Consequences

- No active feature roadmap competes with CodeRAG.
- Migration guidance stays prominent.
- Architecture Reader and other family tools integrate with CodeRAG, not this
  predecessor.

## Verification

- Roadmap added at `docs/roadmap/sota-family-roadmap.md`.
- PROJECT and README link to the roadmap.
- Docs-only validation: `git diff --check`.
