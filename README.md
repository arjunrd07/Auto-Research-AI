
#  AutoResearch AI: Intelligent Research Automation Platform

**AutoResearch AI** is a modular, agentic framework designed to solve academic information density through automated discovery, LLM-driven synthesis, and event-driven orchestration[cite: 3].

---

##  The Problem: "The Researcher's Bottleneck"
*   **Exponential Volume**: Over 3,000 papers are uploaded to arXiv daily, making manual tracking physically impossible[cite: 3].
*   **The "Cold Start" Problem**: Identifying research gaps requires reading dozens of abstracts before a single novel question can be formulated[cite: 3].
*   **Fragmented Tooling**: Researchers typically jump between search engines, PDF readers, and email clients, losing 40% of their productivity to context switching
---

##  System Architecture & Logic Flow

### 1. High-Level Data Flow
The platform operates as a circular feedback loop rather than a linear pipeline[cite: 3]:

> **Discovery** (arXiv API) → **Ingestion** (FastAPI) → **Intelligence** (BART/Mistral) → **Orchestration** (n8n) → **Delivery** (Telegram/Email) → **Action** (User Feedback)[cite: 3].

### 2. Detailed Technical Architecture
```mermaid
graph TD
    A[arXiv API] -->|Search/Monitor| B(ArXiv Service)
    B -->|JSON Data| C{FastAPI Backend}
    C -->|Store| D[(SQLite DB)]
    
    subgraph  "AI Intelligence Layer"
    E[BART-Large-CNN] ---|Abstractive Summary| C
    F[Mistral-7B] ---|Gap Detection & Outreach|
    
    subgraph "Orchestration Layer"
    G[n8n Workflows] ---|Webhooks| C
    G -->|Parallel Exec| H[Email/Telegram]
    end
    
    I[Streamlit Dashboard] ---|User Control| C
    J[CLI Tool] ---|Direct Access| C
```

---

## 💡 The Approach: "Agentic Modularity"
This platform moves away from "hard-coded" logic by using **n8n** as a state machine[cite: 3]:
1.  **Distributed Intelligence**: Uses **BART-large-CNN** for deterministic summarization (avoiding hallucinations in facts) and **Mistral-7B** for creative reasoning (gap detection)[cite: 3].
2.  **Stateful Orchestration**: n8n workflows manage **Conditional Branching**—for example, only sending a Telegram alert if the AI detects high semantic relevance to a user's active projects[cite: 3].
3.  **Graceful Degradation**: If the HuggingFace API is rate-limited, the system automatically triggers **Extractive Fallbacks**, ensuring the user still receives a summary even without the LLM[cite: 3].

---

## 🔑 Key Features & Engineering Innovation
*   **5 Production-Ready Workflows**: Includes a **Multi-Topic Monitor** that fires only when a threshold of $\ge 3$ papers is met, preventing notification fatigue[cite: 3].
*   **Research Gap Webhooks**: A dedicated `/webhook/gap-analysis` endpoint allows external tools to trigger the Mistral-7B reasoning engine on-demand[cite: 3].
*   **One-Click Deployment**: Includes a `start.bat` and `start.sh` system that launches the FastAPI backend, Streamlit UI, and n8n environment simultaneously[cite: 3].
*   **Headless Capability**: A full-featured **CLI tool** allows for serverless operation and automated database maintenance via terminal[cite: 3].

---

## 🚀 Deployment & Installation

### 1. Quick Start
```bash
# Clone and prepare environment
git clone https://github.com/arjunrd07/AutoResearch-AI
cd autoresearch-ai
pip install -r requirements.txt

# Configure AI engine
echo "HUGGINGFACE_API_TOKEN=your_token_here" >> .env
```
[cite: 3]

### 2. Workflow Activation
1. Start n8n: `n8n start`[cite: 3].
2. Import the JSON files from `/n8n/workflows/`[cite: 3].
3. Add your SMTP/Telegram credentials in the n8n UI[cite: 3].

---

## 🎯 Conclusion & Impact
**AutoResearch AI** demonstrates that the value of AI is not just in the "model," but in the **orchestration**[cite: 3]. By delegating discovery and synthesis to an automated agent, researchers can focus 100% of their energy on **experimentation and writing**[cite: 3]. The system successfully reduces the weekly research monitoring time from ~10 hours to under 30 minutes of "reviewing" automated digests[cite: 3].

---

## 🔮 Future Roadmap
*   **Vision-Integrated Research**: Utilizing **Llama 4 Scout** to analyze charts and figures within PDFs alongside text
*   **Multi-Agent Consensus**: Implementing a synthesis layer where multiple LLMs (Mistral, Llama) "debate" the research gaps to increase accuracy
*   **Local Inference**: Integration with **Ollama** for users who require 100% data privacy with no external API calls