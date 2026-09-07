# 🧠 AI Research & Deep Agent Assistant

An AI-powered research assistant built with **Python, LangChain, LangGraph, Deep Agents, Groq, Tavily, and Streamlit**.

The project explores how an AI assistant can go beyond a simple question-and-answer chatbot by combining **planning, web search, skills, subagents, memory, file handling, and structured outputs** into one application.

---

## 🚀 Features

- 🧠 **Deep Agent orchestration** for multi-step tasks
- 📋 **Agentic planning** using `write_todos`
- 🔎 **Web research** using Tavily
- 🤖 **Specialized subagents** for deeper research
- 🧩 **Skills-based context** for reusable domain instructions
- 📁 **Virtual file system** for handling intermediate information
- 📝 **AGENTS.md context** for project-specific instructions
- 💾 **Thread-based memory** using LangGraph checkpointing
- 🗃️ **Multiple backend options**
  - StateBackend
  - FilesystemBackend
  - StoreBackend
- 📦 **Structured output** using Pydantic
- 🎛️ **Configurable Streamlit interface**
- ⚡ **Groq-powered LLM inference**

---

## 🏗️ Architecture

```text
                         ┌──────────────────────┐
                         │        User          │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │      Streamlit       │
                         │         UI           │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │     Deep Agent       │
                         └──────────┬───────────┘
                                    │
              ┌─────────────────────┼─────────────────────┐
              │                     │                     │
              ▼                     ▼                     ▼
        ┌───────────┐        ┌─────────────┐       ┌─────────────┐
        │ Planning  │        │ Web Search  │       │  Subagents  │
        │           │        │   Tavily    │       │ Specialized │
        │ write_    │        └─────────────┘       │   Research  │
        │ todos     │                              └─────────────┘
        └───────────┘
              │
              ▼
        ┌─────────────────────────────────────────────┐
        │           Context & File Management         │
        │                                             │
        │ • Skills                                   │
        │ • AGENTS.md                                │
        │ • Virtual Files                            │
        │ • Memory / Checkpointing                   │
        │ • State / Filesystem / Store Backends     │
        └──────────────────────┬──────────────────────┘
                               │
                               ▼
                    ┌────────────────────────┐
                    │     Final Response     │
                    └────────────────────────┘
```

---

## 🛠️ Tech Stack

| Technology | Purpose |
|---|---|
| **Python** | Core programming language |
| **Streamlit** | Web application interface |
| **LangChain** | LLM and tool integration |
| **LangGraph** | Agent state and workflow management |
| **Deep Agents** | Agent orchestration, planning, files, and subagents |
| **Groq** | LLM inference |
| **Tavily** | Web search and research |
| **Pydantic** | Structured outputs and validation |
| **UV** | Python environment and dependency management |

---

## 🔄 How It Works

A typical request follows this flow:

```text
User Question
      ↓
Deep Agent
      ↓
Understand the task
      ↓
Plan when necessary
      ↓
Choose tools / skills / subagents
      ↓
Research or perform file operations
      ↓
Combine the results
      ↓
Final Response
```

For research-heavy tasks:

```text
User
 ↓
Planning
 ↓
Tavily Web Search
 ↓
Research Subagent
 ↓
Structured Findings
 ↓
Final Answer
```

---

## 🧠 Deep Agent Capabilities

### 📋 Planning

The agent can use `write_todos` to break complex tasks into smaller steps and track their progress.

### 🔎 Web Research

The assistant can use Tavily to search the web when external information is needed.

### 🤖 Subagents

The main agent can delegate specialized work to separate research agents.

The project currently includes:

- `research-agent`
- `structured-researcher`

The structured researcher uses a Pydantic schema to return structured findings.

### 🧩 Skills

Reusable skills are stored in the `skills/` directory.

Current skill areas include:

- AWS
- LangGraph
- Python
- Report Writer

### 📁 Context and File Management

The agent can work with:

- `AGENTS.md`
- Skills
- Virtual files
- Intermediate files
- Memory

This allows larger tasks to be handled without putting every intermediate result directly into the conversation.

### 💾 Memory

LangGraph checkpointing is used to maintain conversation state across turns.

The application also supports creating a new conversation thread when a fresh context is required.

### 🗃️ Backend Options

The application supports three backend approaches:

```text
StateBackend
FilesystemBackend
StoreBackend
```

This makes the agent's file and memory behavior configurable.

---

## 📂 Project Structure

```text
AI-Research-Deep-Agent/
│
├── streamlit_app.py
├── README.md
├── .gitignore
│
├── skills/
│   ├── aws/
│   ├── langgraph/
│   ├── python/
│   └── report-writer/
│
└── projects/
    └── AGENTS.md
```

### `streamlit_app.py`

The main Streamlit application containing the agent configuration, tools, memory, skills, subagents, and user interface.

### `skills/`

Reusable skill instructions that provide additional context for specific tasks.

### `projects/AGENTS.md`

Project-level instructions and architectural context used by the Deep Agent.

---

## ⚙️ Setup

### 1. Clone the repository

```bash
git clone https://github.com/Harshitraj123/AI-Research-Deep-Agent.git
cd AI-Research-Deep-Agent
```

### 2. Install dependencies

This project uses UV for dependency management:

```bash
uv sync
```

### 3. Configure environment variables

Create a `.env` file in the project root:

```env
GROQ_API_KEY=your_groq_api_key
TAVILY_API_KEY=your_tavily_api_key
```

Never commit your actual `.env` file or API keys.

---

## ▶️ Run the Application

Start the Streamlit application with:

```bash
uv run python -m streamlit run streamlit_app.py
```

The application will open in your browser.

---

## 🎛️ Configuration

The Streamlit sidebar allows you to configure:

- LLM model
- Backend
- AGENTS.md context
- Skills
- Subagents
- System prompt
- Conversation threads

This makes it easy to experiment with different agent configurations without modifying the core application.

---

## 💡 Example Tasks

The assistant can handle tasks such as:

```text
Research the latest developments in LangGraph.

Explain how AWS EC2 works and provide a step-by-step guide.

Research a technical topic and summarize the important findings.

Use the Python skill to help debug a piece of code.

Create a structured research report about a technology.
```

---

## 📚 Key Concepts Demonstrated

This project focuses on practical implementation of:

- Agentic workflows
- LangGraph state management
- Deep Agent architecture
- Tool calling
- Context engineering
- Planning and task decomposition
- Subagent delegation
- Structured outputs
- Web research
- Memory and checkpointing
- Virtual file systems
- Backend abstraction
- Streamlit application development

---

## 🔮 Future Improvements

Planned improvements include:

- Additional specialized agents
- Persistent production-grade storage
- Better source verification and citation handling
- Authentication and user-specific memory
- Production deployment
- Automated evaluation of research quality

---

## 👨‍💻 Author

**Harshit Raj**

Built as part of my hands-on work in:

**Generative AI • LangChain • LangGraph • Agentic AI**

---

## ⭐ Support

If you find the project useful, consider giving the repository a ⭐ on GitHub.