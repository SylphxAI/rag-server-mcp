# SOTA Family Roadmap

Status: deprecated adoption plan
Owner: RAG Server MCP
Scope: repo-local future plan and its role in the SylphxAI MCP family
Decision record: `docs/adr/ADR-4-mcp-family-sota-roadmap.md`

## Family Role

RAG Server MCP is the deprecated predecessor to CodeRAG. It is not an active
member of the future MCP suite except as a migration marker.

## Family Fit

| Project                 | Relationship                                                                           |
| ----------------------- | -------------------------------------------------------------------------------------- |
| CodeRAG                 | Successor and owner of current code retrieval, indexing, ranking, and MCP search.      |
| Architecture Reader MCP | No dependency; architecture intelligence should integrate with CodeRAG, not this repo. |
| Consultant MCP          | May cite this repository only as historical migration context.                         |

## SOTA End State

The SOTA path is retirement, not revival. Users should migrate to CodeRAG, and
new code search investment should happen there. The future code-retrieval MCP
runtime should be Rust using `modelcontextprotocol/rust-sdk` / `rmcp`; this
deprecated repository should not grow a new TypeScript adapter roadmap.

## Roadmap

### Phase 0: Migration Clarity

- Keep README focused on migration to CodeRAG.
- Avoid claims that imply active support.
- Add a project boundary that marks this repo as deprecated.
- Point future MCP runtime work to CodeRAG's Rust server roadmap.

### Phase 1: Package Safety

- Do not publish feature releases.
- If a security fix is unavoidable, release only the minimum forward fix and
  keep migration guidance prominent.

### Phase 2: Archive Hygiene

- Keep the repository archived after docs land.
- Link active family planning to CodeRAG.
- Do not duplicate CodeRAG roadmap or performance claims here.
- Do not add new MCP runtime work here except emergency security forward fixes.

## Validation Gates

- README continues to point to CodeRAG.
- No active roadmap competes with CodeRAG.
- No TypeScript adapter roadmap competes with the Rust MCP family direction.
- Package release remains frozen except for emergency security fixes.
