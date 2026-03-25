# MAS-Blog-Writer

> Autonomous research & blog writing agent powered by LangGraph, Groq, and Tavily.

A hierarchical **Multi-Agent System (MAS)** that autonomously researches any topic on the web and produces a written report or blog post. Just enter a query — the agents handle the rest.

---

## How It Works

A top-level supervisor coordinates two specialized teams, each managed by their own supervisor agent:

```
User Query
    └── Top-Level Supervisor
            ├── Research Team
            │       ├── Search Agent      (Tavily web search)
            │       └── Web Scraper Agent (scrapes URLs for details)
            └── Writing Team
                    ├── Note Taker Agent  (creates outlines)
                    ├── Doc Writer Agent  (writes & edits documents)
                    └── Chart Generator  (runs Python for data/charts)
```

Each agent reasons using **Groq's LLaMA 3.3 70B** model and is given a specific set of tools. The supervisors decide which agent acts next, looping until the task is complete.

---

## Features

- 🔍 **Web search** via Tavily — real-time information retrieval
- 🌐 **Web scraping** — deep-dives into specific URLs for detailed content
- 📝 **Document writing** — creates, reads, and edits text files
- 🗂️ **Outline generation** — structured note-taking before writing
- ⚡ **Powered by Groq** — ultra-fast LLaMA inference
- 🧠 **Hierarchical agents** — modular, extensible multi-agent architecture

---

## Project Structure

```
MAS-Blog-Writer/
├── mas_blog.py         # Main script
├── requirements.txt    # Python dependencies
├── .env.example        # Environment variable template
├── .gitignore
├── README.md
└── agent_docs/         # Auto-created at runtime (agent output files)
```

---

## Setup

### 1. Clone the repo

```bash
git clone https://github.com/your-username/MAS-Blog-Writer.git
cd MAS-Blog-Writer
```

### 2. Create a virtual environment

```bash
python -m venv .venv
source .venv/bin/activate      # macOS/Linux
.venv\Scripts\activate         # Windows
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Set up environment variables

```bash
cp .env.example .env
```

Open `.env` and fill in your API keys:

```env
GROQ_API_KEY=gsk_your_key_here
TAVILY_API_KEY=tvly_your_key_here
```

| Key | Where to get it |
|-----|----------------|
| `GROQ_API_KEY` | [console.groq.com](https://console.groq.com) → API Keys |
| `TAVILY_API_KEY` | [app.tavily.com](https://app.tavily.com) → API Keys |

---

## Usage

```bash
python mas_blog.py
```

You will be prompted to enter a query:

```
============================================================
  Multi-Agent Research & Writing System
  Teams: Research (search + scraper) | Writing (doc + notes + chart)
============================================================

Enter your query: Write a blog post about the rise of AI agents in 2025
```

The agents will run and print their progress step by step. Any documents written by the agents are saved to the `agent_docs/` folder.

### Example queries

```
Research the latest trends in renewable energy and write a detailed report
Write a blog post about the rise of AI agents in 2025
Research Tesla's performance in 2025 and summarize the findings
What are the top 5 programming languages in 2025 and why?
```

---

## Configuration

You can optionally set these in your `.env`:

```env
# Groq model to use (default: llama-3.3-70b-versatile)
GROQ_MODEL=llama-3.1-8b-instant

# Directory where agents save documents (default: ./agent_docs)
AGENT_DOCS_DIR=./agent_docs
```

### Recommended Groq models

| Model | Free Tier TPD | Best For |
|-------|-------------|----------|
| `llama-3.3-70b-versatile` | 100k tokens | Best quality |
| `llama-3.1-8b-instant` | 500k tokens | Testing / high volume |
| `mixtral-8x7b-32768` | 500k tokens | Balanced |

> **Tip:** Use `llama-3.1-8b-instant` during development to avoid hitting the daily token limit, then switch to `llama-3.3-70b-versatile` for final runs.

---

## Requirements

- Python 3.10+
- Groq API key (free tier available)
- Tavily API key (free tier: 1,000 searches/month)

---

## Dependencies

| Package | Purpose |
|---------|---------|
| `langgraph` | Multi-agent graph orchestration |
| `langchain-groq` | Groq LLM integration |
| `langchain-tavily` | Tavily search tool |
| `langchain-community` | Web scraping loader |
| `python-dotenv` | `.env` file loading |

