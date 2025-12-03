# 🤖 AI-Powered Chatbot (LangGraph RAG demo)

🔗 Live demo: https://ai-powered-chatbot-cy18.onrender.com

## 🚀 Quick overview
- 🖥️ Web UI built with Streamlit (`streamlit_rag_frontend.py`).
- 🔧 Backend: `langgraph_rag_backend.py` — implements RAG + tool-enabled agent.
- 🧰 Tools available: calculator (calc), DuckDuckGo web search, and PDF RAG (index & QA).
- 🧠 LLM: Gemini / Google Generative AI (configured in backend).

## 🧩 What `langgraph_rag_backend.py` does (brief)
- `chatbot`: main agent interface — supports streaming and emits AIMessage, HumanMessage, ToolMessage. Accepts message payloads and config (e.g., thread_id).
- `ingest_pdf(bytes, thread_id, filename)`: indexes uploaded PDFs (chunking, embedding, storing metadata).
- `retrieve_all_threads()`: returns past thread IDs for the sidebar.
- `thread_document_metadata(thread_id)`: returns last indexed doc metadata (filename, chunks, pages).
- The backend wires a vectorstore retriever with an agent + toolset — inspect it to change embeddings, storage, or tools.

## 🖼️ Screenshot / UI preview



 Get Acces to : **Screenshot-2025-12-03-123742.jpg**


Short visual description of the UI (how it looks) 🎨
- Left sidebar:
  - Title + current Thread ID 🧾
  - "New Chat" button ➕
  - PDF uploader (index per-thread) 📄
  - List of past threads (buttons) 🔁
  - Current indexed PDF summary (filename, chunks, pages) ✅
- Main area:
  - App title at top (e.g., "Multi Utility Chatbot") 🏷️
  - Chat messages rendered in conversation style (user/assistant) 💬
  - Streamed assistant responses with tool usage indicator (status box) ⚙️
  - Chat input at bottom to send queries ✍️

## 🛠️ Local installation (Windows) — concise
1. Install Python 3.10+.
2. Clone repo and open PowerShell/CMD in project folder.
3. Create & activate venv:
   - python -m venv .venv
   - PowerShell: .\.venv\Scripts\Activate.ps1
   - CMD: .\.venv\Scripts\activate.bat
4. Install dependencies:
   - pip install -r requirements.txt
5. Set environment variables (Gemini / Google AI):
   - PowerShell:
     $env:GEMINI_API_KEY="your_api_key"
     $env:GOOGLE_APPLICATION_CREDENTIALS="C:\path\to\service-account.json"
   - CMD:
     set GEMINI_API_KEY=your_api_key
     set GOOGLE_APPLICATION_CREDENTIALS=C:\path\to\service-account.json
6. Run:
   - streamlit run streamlit_rag_frontend.py --server.port 8501
   - Open http://localhost:8501

## 💡 Usage notes
- Upload a PDF in the sidebar to index it for the current thread 📎.
- Ask questions in the chat input — the agent may call tools (calc, DuckDuckGo) and stream tool usage 🔄.
- "New Chat" creates a fresh thread_id; click past-thread buttons to load history.

## ✍️ Example prompts
- "Summarize the uploaded document." 📝
- "Find references to 'pricing' and summarize." 🔎
- "Calculate: 345*12" 🧮
- "Search web for 'current LangChain release'." 🌐

## ⚠️ Troubleshooting
- Async loop errors: ensure correct Python interpreter (activated venv). The frontend attempts to set an event loop for Streamlit.
- Missing API creds: set env vars and restart Streamlit.
- Import issues: ensure `langgraph_rag_backend.py` is reachable (same folder or PYTHONPATH).
- Embeddings/vectorstore failures: check provider config and storage paths.

## 🔍 Extending / debugging
- Add/change tools or modify the agent in `langgraph_rag_backend.py`.
- Change LLM settings (model, temperature) in backend LLM client creation.
- Keep API keys out of source control.

## 📎 Live demo
- https://ai-powered-chatbot-cy18.onrender.com
