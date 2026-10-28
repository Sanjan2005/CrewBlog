# ✍️ Blog Writing Crew

An autonomous, multi-agent blog generation pipeline built with [CrewAI](https://crewai.com) and powered by Google Gemini. This project utilizes CrewAI's modern **JSON-first architecture** to orchestrate specialized AI agents that collaboratively research, draft, and edit publication-ready, long-form articles from any given topic.

---

## 🚀 Workflow Overview

The crew executes in a sequential multi-agent loop where each agent builds on the previous agent's output:

```
[ User Input: {topic} ]
          │
          ▼
┌──────────────────────────────┐
│    Research Analyst Agent    │ ──> Gathers facts, statistics, and industry trends
└──────────────┬───────────────┘
               │ (Research Brief)
               ▼
┌──────────────────────────────┐
│      Blog Writer Agent       │ ──> Drafts structured, compelling article with headings
└──────────────┬───────────────┘
               │ (Draft Post)
               ▼
┌──────────────────────────────┐
│ Senior Content Editor Agent  │ ──> Polishes flow, checks grammar, refines readability
└──────────────┬───────────────┘
               │
               ▼
[ Output: output/blog_post.md ]
```

---

## 👥 Agents & Responsibilities

| Agent | Role | Objective |
| :--- | :--- | :--- |
| **Topic Research Analyst** | `{topic} Research Analyst` | Conducts thorough background research on the target topic, compiling 8–10 key points, statistics, and angles. |
| **Topic Blog Writer** | `{topic} Blog Writer` | Translates research notes into an accessible, engaging 800–1000 word blog post with clear headers and narratives. |
| **Senior Content Editor** | `Senior Content Editor` | Polishes the draft for tone consistency, structural flow, clarity, and formatting, delivering the final markdown. |

---

## 🛠️ Tech Stack

- **Orchestration**: [CrewAI](https://crewai.com) (`v1.15+`) with JSONC declarative configuration (`crew.jsonc`, `agents/*.jsonc`).
- **Language Model**: [Google Gemini](https://ai.google.dev/) via `google-genai` integration (`gemini/gemini-3.5-flash`).
- **Environment & Package Management**: [Astral `uv`](https://docs.astral.sh/uv/) for high-speed dependency resolution and virtual environments.
- **Python**: `>=3.10, <3.14`
- **Output Format**: Markdown (`.md`) saved directly to `output/`.

---

## 📂 Project Structure

```text
blog_writing_crew/
├── agents/                           # Agent definitions (JSONC format)
│   ├── senior_content_editor.jsonc
│   ├── topic_blog_writer.jsonc
│   └── topic_research_analyst.jsonc
├── knowledge/                        # Knowledge base files injected into agent prompts
│   └── user_preference.txt
├── output/                           # Generated articles and markdown exports
│   └── blog_post.md
├── tools/                            # Custom Python tools for agents
├── crew.jsonc                        # Core crew configuration, tasks, and default inputs
├── pyproject.toml                    # Python project configuration and dependencies
├── uv.lock                           # Locked dependency tree
├── .env.example                      # Template for required environment variables
└── README.md                         # Project documentation
```

---

## ⚙️ Getting Started

### 1. Prerequisites

- Python `>= 3.10`
- [uv](https://docs.astral.sh/uv/) installed:
  ```bash
  # Windows (PowerShell)
  powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
  ```
- A Google AI Studio API Key ([Get one here](https://aistudio.google.com/app/apikey))

### 2. Installation

Clone the repository and install dependencies using `uv`:

```bash
git clone https://github.com/Sanjan2005/CrewBlog.git
cd CrewBlog
uv sync
```

### 3. Environment Setup

Create a `.env` file in the project root:

```env
MODEL=gemini/gemini-3.5-flash
GEMINI_API_KEY=your_google_gemini_api_key_here
```

> **Security Note:** The `.env` file is excluded in `.gitignore` to prevent secret leaks. Never commit your API keys.

---

## 💻 Usage

Run the crew using the CrewAI CLI:

```bash
crewai run
```

### Customizing the Topic

To change the topic, update the `inputs` section at the bottom of `crew.jsonc`:

```jsonc
"inputs": {
  "topic": "The Future of AI Agents in Software Engineering"
}
```

Or leave it blank to let `crewai run` prompt you interactively in the terminal.

The finished publication-ready post will be saved to `output/blog_post.md`.

---

## 📄 License

This project is open-source under the MIT License.
