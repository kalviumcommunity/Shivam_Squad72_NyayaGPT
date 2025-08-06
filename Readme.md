# 🤖 NyayaGPT — AI Legal Assistant for Indian Laws 🇮🇳

NyayaGPT is an AI-powered assistant designed to help Indian citizens understand laws, rights, legal procedures, and court-related queries using natural language. It simplifies complex legal jargon into human-friendly explanations and provides structured responses, legal references, and step-by-step guidance — all powered by state-of-the-art LLM techniques like Function Calling and Retrieval-Augmented Generation (RAG).

---

## 🌟 Key Features

- Ask legal questions in English or Hindi
- Get step-by-step legal processes in bullet points
- Receive legal references (Acts, Sections)
- Automatically fetch recent legal articles, judgments (via RAG)
- Use of advanced LLM capabilities: System/User Prompting, Function Calling, Structured Outputs

---

## 🎯 Project Objective

To build an interactive legal chatbot that helps users understand:
- Procedures like filing an RTI, FIR, consumer complaints, etc.
- What laws apply in a particular situation
- What penalties or rights they may have
- Latest updates in Indian legal framework using RAG

---

## 🧠 Concept Implementations

### 1. 🧾 Prompting (System Prompt & User Prompt)

We use **System Prompts** to set the AI’s behavior, tone, and purpose. This helps maintain consistency and domain alignment (legal domain in this case).

**System Prompt Example**:
```
You are NyayaGPT, an AI legal assistant. You explain Indian legal procedures in simple language. Always give bullet points, act references, and suggest next steps.
```

**User Prompt Example**:
```
What is the process of filing a consumer complaint in Delhi?
```

The prompts are sent to the model using an API (e.g., OpenAI's Chat API), and fine-tuned for temperature and max tokens.

---

### 2. 📊 Structured Output

The assistant responds in a structured JSON format that is easy to parse and display on frontend.

**Example Output**:
```json
{
  "question": "How to file a consumer complaint in Delhi?",
  "steps": [
    "Determine the jurisdiction based on claim value.",
    "Prepare a complaint with evidence and invoices.",
    "Pay the fee as per Consumer Protection Rules.",
    "Submit via online portal or in-person."
  ],
  "legal_reference": {
    "act": "Consumer Protection Act, 2019",
    "sections": ["Section 17", "Section 21"]
  }
}
```

This structure helps us:
- Build FAQ sections
- Render step-by-step guides in UI
- Allow other systems to consume the API

---

### 3. ⚙️ Function Calling

The project uses **OpenAI-style Function Calling** to trigger backend functions when needed.

**Example Use Case**:
> "What is the court fee if I file a ₹2,00,000 complaint in Bangalore?"

LLM parses the intent and calls this backend function:
```python
def get_court_fee(city: str, claim_amount: float) -> str:
    ...
```

The LLM will return:
```json
{
  "function_call": {
    "name": "get_court_fee",
    "arguments": {
      "city": "Bangalore",
      "claim_amount": 200000
    }
  }
}
```

This helps connect legal logic and data into live conversations.

---

### 4. 📚 Retrieval-Augmented Generation (RAG)

The assistant uses RAG to fetch real legal texts, case summaries, and documents from Indian legal databases and official PDFs.

**Workflow**:
1. Upload PDFs or scrape legal sites (e.g., eCourts, IndiaCode).
2. Break them into chunks and convert to embeddings using a model like `all-MiniLM-L6-v2`.
3. Store embeddings in a vector DB (like **ChromaDB** or **FAISS**).
4. On query, fetch top-k relevant chunks and add them to the prompt context.

**Example Query**:
> “What does the law say about cyberbullying in India?”

RAG injects context like:
> “According to Section 66A of the IT Act...”

LLM then generates an answer with more accuracy and legal backing.

---

## 🛠 Tech Stack

- **Frontend**: React.js + Tailwind CSS
- **Backend**: Node.js / Python (Flask or FastAPI)
- **LLM API**: OpenAI / Ollama
- **Vector DB**: ChromaDB or FAISS
- **Embeddings**: SentenceTransformers
- **PDF Parser**: PyMuPDF or Unstructured.io

---

## 📌 Future Plans

- Add regional language support (e.g., Hindi, Tamil)
- Voice-based queries (via Whisper or Web Speech API)
- Real-time updates from court databases
- Option to download legal steps as PDFs

---
