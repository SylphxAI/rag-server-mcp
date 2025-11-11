<div align="center">

# RAG Server MCP 📚

**Local-first Retrieval Augmented Generation for AI agents - Privacy-focused with automatic indexing**

[![npm version](https://img.shields.io/npm/v/@sylphlab/mcp-rag-server?style=flat-square)](https://www.npmjs.com/package/@sylphlab/mcp-rag-server)
[![CI Status](https://img.shields.io/github/actions/workflow/status/SylphxAI/rag-server-mcp/typescript-ci.yml?style=flat-square)](https://github.com/SylphxAI/rag-server-mcp/actions/workflows/typescript-ci.yml)
[![License](https://img.shields.io/badge/License-MIT-blue?style=flat-square)](https://github.com/SylphxAI/rag-server-mcp/blob/main/LICENSE)

**Local models** • **Automatic indexing** • **ChromaDB vectors** • **5 MCP tools**

[Quick Start](#-quick-start) • [Installation](#-installation) • [Tools](#-mcp-tools)

<a href="https://glama.ai/mcp/servers/@sylphlab/mcp-rag-server">
  <img width="380" height="200" src="https://glama.ai/mcp/servers/@sylphlab/mcp-rag-server/badge" alt="RAG Server MCP" />
</a>

</div>

---

## 🚀 Overview

Enable your AI agents with powerful Retrieval Augmented Generation (RAG) capabilities using local models. This [Model Context Protocol (MCP)](https://modelcontextprotocol.io) server automatically indexes your project documents and provides relevant context to enhance LLM responses.

**The Problem:**
```
Traditional RAG solutions:
- Cloud-based (privacy concerns) ❌
- Complex setup (multiple services) ❌
- Manual indexing (time-consuming) ❌
- Expensive API costs (per query) ❌
```

**The Solution:**
```
RAG Server MCP:
- Local-first (Ollama + ChromaDB) ✅
- Docker Compose (one command) ✅
- Automatic indexing (on startup) ✅
- Free local models (zero API costs) ✅
```

**Result: Privacy-focused, zero-cost RAG with automatic context retrieval for your AI agents.**

---

## ⚡ Key Advantages

### Privacy & Control

| Feature | Cloud RAG | RAG Server MCP |
|---------|-----------|----------------|
| **Data Privacy** | ❌ Sent to cloud | ✅ 100% local |
| **Model Control** | ❌ Fixed models | ✅ Any Ollama model |
| **Vector Storage** | ❌ Cloud service | ✅ Local ChromaDB |
| **Cost** | ❌ Pay per query | ✅ Free (local) |
| **Customization** | ⚠️ Limited | ✅ Full control |

### Performance & Efficiency

- **Automatic Indexing** - Scans project on startup, no manual work
- **Persistent Vectors** - ChromaDB stores embeddings between sessions
- **Hierarchical Chunking** - Smart markdown splitting (text + code blocks)
- **Multiple File Types** - `.txt`, `.md`, code files, `.json`, `.csv`
- **Local Embeddings** - Ollama `nomic-embed-text` (no API calls)

---

## 📦 Installation

### Method 1: Docker Compose (Recommended)

Run the server and all dependencies (ChromaDB, Ollama) in isolated containers.

**Prerequisites:**
- [Docker Desktop](https://www.docker.com/products/docker-desktop/) or Docker Engine
- Ports `8000` (ChromaDB) and `11434` (Ollama) available

**Setup:**

```bash
# Clone repository
git clone https://github.com/SylphxAI/rag-server-mcp.git
cd rag-server-mcp

# Start all services
docker-compose up -d --build

# Pull embedding model (first run only)
docker exec ollama ollama pull nomic-embed-text
```

### Method 2: npx (Requires External Services)

If you already have ChromaDB and Ollama running:

```bash
# Set environment variables
export CHROMA_URL=http://localhost:8000
export OLLAMA_HOST=http://localhost:11434

# Run via npx
npx @sylphlab/mcp-rag-server
```

### Method 3: Local Development

```bash
# Clone and install
git clone https://github.com/SylphxAI/rag-server-mcp.git
cd rag-server-mcp
npm install

# Build
npm run build

# Start (requires ChromaDB + Ollama)
npm start
```

---

## 🚀 Quick Start

### MCP Client Configuration

Add to your MCP client configuration (e.g., Claude Desktop, Cline):

```json
{
  "mcpServers": {
    "rag-server": {
      "command": "npx",
      "args": ["@sylphlab/mcp-rag-server"],
      "env": {
        "CHROMA_URL": "http://localhost:8000",
        "OLLAMA_HOST": "http://localhost:11434",
        "INDEX_PROJECT_ON_STARTUP": "true"
      }
    }
  }
}
```

**Note:** With Docker Compose, the server runs in a container. You may need to expose the MCP port or configure network settings for external client access.

### Basic Usage

Once configured, your AI agent can use RAG tools:

```xml
<!-- Index project documents -->
<use_mcp_tool>
  <server_name>rag-server</server_name>
  <tool_name>indexDocuments</tool_name>
  <arguments>{"path": "./docs"}</arguments>
</use_mcp_tool>

<!-- Query for relevant context -->
<use_mcp_tool>
  <server_name>rag-server</server_name>
  <tool_name>queryDocuments</tool_name>
  <arguments>{"query": "how to configure embeddings", "topK": 5}</arguments>
</use_mcp_tool>

<!-- List indexed documents -->
<use_mcp_tool>
  <server_name>rag-server</server_name>
  <tool_name>listDocuments</tool_name>
</use_mcp_tool>
```

---

## 🛠️ MCP Tools

### Document Management

| Tool | Description | Parameters |
|------|-------------|------------|
| **indexDocuments** | Index file or directory | `path`, `forceReindex?` |
| **queryDocuments** | Retrieve relevant chunks | `query`, `topK?`, `filter?` |
| **listDocuments** | List all indexed sources | None |
| **removeDocument** | Remove document by path | `sourcePath` |
| **removeAllDocuments** | Clear entire index | None |

### Tool Details

**indexDocuments**
```typescript
{
  path: string;          // File or directory path
  forceReindex?: boolean; // Re-index if already indexed
}
```

**queryDocuments**
```typescript
{
  query: string;    // Search query
  topK?: number;    // Number of results (default: 5)
  filter?: object;  // Metadata filters
}
```

**Supported File Types:**
- **Text**: `.txt`, `.md`
- **Code**: `.ts`, `.js`, `.py`, `.java`, `.go`, etc.
- **Data**: `.json`, `.jsonl`, `.csv`

---

## ⚙️ Configuration

Configure via environment variables (set in `docker-compose.yml` or CLI):

### Core Settings

| Variable | Default | Description |
|----------|---------|-------------|
| **CHROMA_URL** | `http://chromadb:8000` | ChromaDB service URL |
| **OLLAMA_HOST** | `http://ollama:11434` | Ollama service URL |
| **INDEX_PROJECT_ON_STARTUP** | `true` | Auto-index on server start |
| **GENKIT_ENV** | `production` | Environment mode |
| **LOG_LEVEL** | `info` | Logging level |

### Indexing Configuration

| Variable | Default | Description |
|----------|---------|-------------|
| **INDEXING_EXCLUDE_PATTERNS** | `**/node_modules/**,**/.git/**` | Glob patterns to exclude |

**Example Custom Config:**

```yaml
# docker-compose.yml
services:
  rag-server:
    environment:
      - INDEX_PROJECT_ON_STARTUP=true
      - INDEXING_EXCLUDE_PATTERNS=**/node_modules/**,**/.git/**,**/dist/**
      - LOG_LEVEL=debug
```

---

## 🏗️ Architecture

### Technology Stack

| Component | Technology | Purpose |
|-----------|-----------|---------|
| **Framework** | [Google Genkit](https://firebase.google.com/docs/genkit) | RAG orchestration |
| **Vector Store** | [ChromaDB](https://www.trychroma.com/) | Persistent embeddings |
| **Embeddings** | [Ollama](https://ollama.com/) | Local embedding models |
| **Protocol** | Model Context Protocol | AI agent integration |
| **Language** | TypeScript | Type-safe development |

### How It Works

```
┌─────────────────────────────────────────────────────────┐
│ 1. Document Indexing (Startup or Manual)               │
│    • Scan project directory                            │
│    • Chunk documents hierarchically                    │
│    • Generate embeddings via Ollama                    │
│    • Store vectors in ChromaDB                         │
└─────────────────┬───────────────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────────────────┐
│ 2. Query Processing (AI Agent Request)                 │
│    • Receive query from MCP client                     │
│    • Generate query embedding                          │
│    • Search ChromaDB for similar vectors              │
│    • Return top-K relevant chunks                      │
└─────────────────┬───────────────────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────────────────┐
│ 3. Context Enhancement (AI Agent Uses Results)         │
│    • Relevant context injected into prompt             │
│    • LLM generates informed response                   │
└─────────────────────────────────────────────────────────┘
```

---

## 🎯 Use Cases

### AI Code Assistants
- **Codebase understanding** - Query project architecture
- **API documentation** - Find relevant API docs
- **Code examples** - Retrieve similar code patterns
- **Dependency info** - Search package documentation

### Knowledge Management
- **Documentation search** - Find relevant docs instantly
- **Technical notes** - Index personal knowledge base
- **Meeting notes** - Search past discussions
- **Research papers** - Index and query papers

### Development Workflows
- **Onboarding** - Help new developers understand codebase
- **Code review** - Find related code for context
- **Bug fixing** - Search for similar issues
- **Feature development** - Discover existing patterns

---

## 📊 Design Philosophy

### Core Principles

**1. Local-First**
- All processing happens on your machine
- No data sent to cloud services
- Use your own hardware and models

**2. Simplicity**
- One-command Docker Compose setup
- Automatic indexing by default
- Sensible defaults for all settings

**3. Modularity**
- Genkit flows organize RAG logic
- Pluggable embedding models
- Extensible file type support

**4. Privacy**
- Your documents never leave your machine
- Local embedding generation
- Local vector storage

---

## 🔧 Development

### Setup

```bash
# Install dependencies
npm install

# Build
npm run build

# Watch mode
npm run watch
```

### Quality Checks

```bash
# Lint code
npm run lint

# Format code
npm run format

# Run tests
npm test

# Test with coverage
npm run test:cov

# Validate all (format + lint + test)
npm run validate
```

### Documentation

```bash
# Dev server
npm run docs:dev

# Build docs
npm run docs:build

# Preview docs
npm run docs:preview
```

---

## 🗺️ Roadmap

**✅ Completed**
- [x] MCP server implementation
- [x] ChromaDB integration
- [x] Ollama local embeddings
- [x] Automatic indexing on startup
- [x] Hierarchical markdown chunking
- [x] Docker Compose setup
- [x] 5 core MCP tools

**🚀 Planned**
- [ ] Advanced code file chunking (AST-based)
- [ ] PDF file support
- [ ] Enhanced query filtering
- [ ] Multiple embedding model support
- [ ] Performance benchmarks
- [ ] Semantic caching
- [ ] Re-ranking for better relevance
- [ ] Web UI for index management

---

## 🤝 Contributing

Contributions are welcome! Please follow these guidelines:

1. **Open an issue** - Discuss changes before implementing
2. **Fork the repository**
3. **Create a feature branch** - `git checkout -b feature/my-feature`
4. **Follow coding standards** - Run `npm run validate`
5. **Write tests** - Ensure good coverage
6. **Submit a pull request**

### Development Guidelines

- Follow TypeScript strict mode
- Use ESLint and Prettier (auto-configured)
- Add tests for new features
- Update documentation
- Follow commit conventions

---

## 🤝 Support

[![npm](https://img.shields.io/npm/v/@sylphlab/mcp-rag-server?style=flat-square)](https://www.npmjs.com/package/@sylphlab/mcp-rag-server)
[![GitHub Issues](https://img.shields.io/github/issues/SylphxAI/rag-server-mcp?style=flat-square)](https://github.com/SylphxAI/rag-server-mcp/issues)

- 🐛 [Bug Reports](https://github.com/SylphxAI/rag-server-mcp/issues)
- 💬 [Discussions](https://github.com/SylphxAI/rag-server-mcp/discussions)
- 📧 [Email](mailto:hi@sylphx.com)
- 📖 [MCP Documentation](https://modelcontextprotocol.io)

**Show Your Support:**
⭐ Star • 👀 Watch • 🐛 Report bugs • 💡 Suggest features • 🔀 Contribute

---

## 📄 License

MIT © [Sylphx](https://sylphx.com)

---

## 🙏 Credits

Built with:
- [Model Context Protocol](https://modelcontextprotocol.io) - AI agent standard
- [Google Genkit](https://firebase.google.com/docs/genkit) - RAG framework
- [ChromaDB](https://www.trychroma.com/) - Vector database
- [Ollama](https://ollama.com/) - Local LLM runtime
- [TypeScript](https://typescriptlang.org) - Type safety

Special thanks to the MCP and Genkit communities ❤️

---

<p align="center">
  <strong>Local. Private. Powerful.</strong>
  <br>
  <sub>RAG capabilities for AI agents with zero cloud dependencies</sub>
  <br><br>
  <a href="https://sylphx.com">sylphx.com</a> •
  <a href="https://x.com/SylphxAI">@SylphxAI</a> •
  <a href="mailto:hi@sylphx.com">hi@sylphx.com</a>
</p>
