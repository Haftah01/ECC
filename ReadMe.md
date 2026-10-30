# Phd. Academic Research Agent 🎓🤖

An advanced, stateful, multi-agent research assistant designed to automate academic literature discovery, synthesis, and structured thesis drafting. Built specifically to support rigorous scholarly writing with domain-specific adaptability.

---

## 🚀 Key Features

* **Planner-Writer Split Architecture:** Uses a fast, lightweight reasoning model (**Llama 3.3 70B**) for tool orchestration and planning, and a deep-context synthesis model (**DeepSeek / Llama 3.1 70B**) for producing formal academic prose.
* **Specialized Tool Suite:** Integrates four distinct data engines:
  * **Semantic Scholar API:** Core citation graph and paper metadata (protected by a strict 1 request/second queue limiter).
  * **Exa AI:** Neural semantic search for finding deeply related research papers via vector similarity.
  * **Tavily API:** Real-time web search for live context and academic news.
  * **Parallel API:** Structured multi-step web research extraction.
* **Persistent Checkpointing (`PostgresSaver`):** Unlike standard RAM-based memory, agent state is persisted to a database, ensuring multi-turn conversations and Human-in-the-Loop (HITL) checkpoints survive server restarts.
* **Modular Prompt Library:** Decoupled prompt structure allowing instant domain switching (Computer Science, Agriculture, Humanities, etc.) without altering core execution logic.
* **Human-in-the-Loop (HITL):** Pauses execution to allow user verification of retrieved literature before committing tokens to the final writing phase.

---

## 📂 Project Structure

```text
phd-research-agent/
├── .env                        # API Keys & Database URIs
├── requirements.txt            # Python dependencies
├── app.py                      # Gradio Web UI entrypoint
├── config/
│   └── settings.py             # Global configurations & tool thresholds
├── prompts/
│   ├── phd_default.py          # Core system instructions & formatting rules
│   └── domain_configs.json     # Field-specific vocabulary overrides
├── tools/
│   ├── search_tools.py         # Tavily, Exa, and Parallel tool wrappers
│   ├── scholar_tools.py        # Semantic Scholar integration
│   └── rate_limiters.py        # Token bucket queue & exponential backoff
└── agent/
    ├── state.py                # ResearchState TypedDict schema
    ├── nodes.py                # Orchestrator and Writer node logic
    └── graph.py                # LangGraph StateGraph assembly & DB binding

```

---

## ⚙️ Installation & Local Setup

1. **Clone the repository:**
```bash
git clone [https://github.com/YOUR_USERNAME/phd-research-agent.git](https://github.com/YOUR_USERNAME/phd-research-agent.git)
cd phd-research-agent

```


2. **Install dependencies:**
```bash
pip install -r requirements.txt

```


3. **Configure Environment Variables:**
Create a `.env` file in the root directory:
```env
NVIDIA_API_KEY=your_nvidia_key
TAVILY_API_KEY=your_tavily_key
EXA_API_KEY=your_exa_key
SEMANTIC_SCHOLAR_API_KEY=your_semantic_scholar_key
DATABASE_URL=postgresql://user:password@host:port/dbname

```
