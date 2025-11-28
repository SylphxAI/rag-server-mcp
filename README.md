<div align="center">

# ⚠️ DEPRECATED - Use CodeRAG Instead ⚠️

<br>

## 🚀 This project has evolved into something much better!

<br>

[![New Project](https://img.shields.io/badge/NEW-CodeRAG-blue?style=for-the-badge&logo=github)](https://github.com/SylphxAI/coderag)
[![npm](https://img.shields.io/npm/v/@sylphx/coderag-mcp?style=for-the-badge&label=Install)](https://www.npmjs.com/package/@sylphx/coderag-mcp)

<br>

# 👉 [github.com/SylphxAI/coderag](https://github.com/SylphxAI/coderag) 👈

<br>

</div>

---

## 🎉 Why CodeRAG is 10x Better

We completely rewrote this project from scratch. Here's what you get:

### ⚡ Lightning Fast

| Feature | Old (rag-server-mcp) | New (CodeRAG) |
|---------|---------------------|---------------|
| **Startup** | 10-30s (ChromaDB + Ollama) | **<1s** (no external deps) |
| **Indexing** | Minutes (embedding API calls) | **Seconds** (TF-IDF + optional vectors) |
| **Search** | ~500ms (vector only) | **<50ms** (hybrid search) |
| **Memory** | 500MB+ (ChromaDB) | **<100MB** (SQLite) |

### 🧠 Smarter Search

| Feature | Old | New |
|---------|-----|-----|
| **TF-IDF** | ❌ | ✅ StarCoder2 tokenizer |
| **Vector Search** | ✅ Basic | ✅ Hybrid (TF-IDF + Vector) |
| **Code Understanding** | ❌ Generic | ✅ Code-aware tokenization |
| **Incremental Updates** | ❌ Full rebuild | ✅ Smart diff detection |

### 🔧 Zero Dependencies

```bash
# Old way (painful)
docker-compose up -d      # Start ChromaDB
ollama pull nomic-embed   # Download model
# Wait 30 seconds...

# New way (instant)
npx @sylphx/coderag-mcp
# Done. That's it. 🎉
```

### 🏆 Battle-Tested Accuracy

- **Smoothed IDF** - No term gets ignored (even common ones like `function`)
- **Logarithmic boosting** - Stable ranking without score explosion
- **StarCoder2 tokenizer** - 4.7MB model trained on code
- **Pre-computed magnitudes** - Memory-efficient cosine similarity

---

## 🚀 Migrate in 30 Seconds

### Step 1: Uninstall old

```json
// Remove from your MCP config
{
  "mcpServers": {
    "rag-server": { ... }  // DELETE THIS
  }
}
```

### Step 2: Install new

```json
{
  "mcpServers": {
    "coderag": {
      "command": "npx",
      "args": ["-y", "@sylphx/coderag-mcp"]
    }
  }
}
```

### Step 3: Enjoy 🎉

No Docker. No Ollama. No ChromaDB. Just works.

---

## 📊 Feature Comparison

| Feature | rag-server-mcp | CodeRAG |
|---------|---------------|---------|
| **External Services** | ChromaDB + Ollama | None |
| **Docker Required** | Yes | No |
| **Startup Time** | 10-30s | <1s |
| **Search Algorithm** | Vector only | Hybrid (TF-IDF + Vector) |
| **Code Tokenization** | Generic | StarCoder2 (code-aware) |
| **Incremental Index** | No | Yes |
| **Memory Usage** | 500MB+ | <100MB |
| **Low Memory Mode** | No | Yes (SQL-based) |
| **Offline Support** | No (needs Ollama) | Yes (TF-IDF) |
| **Vector Search** | Required | Optional |
| **Actively Maintained** | ❌ No | ✅ Yes |

---

## 🔗 Links

- **New Repository**: [github.com/SylphxAI/coderag](https://github.com/SylphxAI/coderag)
- **NPM Package**: [@sylphx/coderag-mcp](https://www.npmjs.com/package/@sylphx/coderag-mcp)
- **Documentation**: [CodeRAG README](https://github.com/SylphxAI/coderag#readme)

---

<div align="center">

## ⚠️ This Repository is Archived

**No new features. No bug fixes. No support.**

Use [CodeRAG](https://github.com/SylphxAI/coderag) instead.

<br>

[![Migrate Now](https://img.shields.io/badge/Migrate_Now-CodeRAG-success?style=for-the-badge&logo=github)](https://github.com/SylphxAI/coderag)

<br>

---

<sub>Made with ❤️ by <a href="https://sylphx.com">Sylphx</a></sub>

</div>
