# 📚 TDS Virtual TA – Intelligent API Assistant for IITM Data Science

This project is a virtual Teaching Assistant (TA) that intelligently answers student questions for the **Tools in Data Science (TDS) Jan 2025** course from the IIT Madras Online B.Sc. in Data Science program.

🔗 **Live API Endpoint**: [https://project-fcs4-pmr8aqs7h-anant-sathes-projects.vercel.app/query](https://project-fcs4-pmr8aqs7h-anant-sathes-projects.vercel.app/query)  
📁 **GitHub Repo**: [https://github.com/anantsathe/project](https://github.com/anantsathe/project)

---

## 🚀 Overview

The app uses **Retrieval-Augmented Generation (RAG)** powered by **FastAPI** and **OpenAI GPT-4o-mini** (via [aipipe.org](https://aipipe.org)) to:

- Accept student queries with optional image input
- Search through pre-processed course material and forum posts
- Generate accurate and source-linked answers

---

## 📂 Project Structure

```
├── api/
│   ├── app.py                            # Main FastAPI app
│   └── project-tds-virtual-ta-promptfoo.yaml  # Promptfoo test config
├── downloaded_threads/                   # Scraped Discourse posts (JSON)
├── markdown_files/                       # Scraped course content (Markdown)
├── preprocess.py                         # Script to build the knowledge base
├── knowledge_base.db                     # SQLite database with embeddings (created)
├── requirements.txt                      # Python dependencies
├── vercel.json                           # Vercel deployment config
├── .env                                  # API key (excluded from Git)
```

---

## 📌 Features

- 🔍 Semantic search across course and forum content
- 🧠 GPT-4o-mini-based contextual answers
- 🖼️ Multimodal (text + base64 image) support
- 🔗 Returns source URLs and snippets
- 🔐 API key protected
- ✅ Health check endpoint `/health`

---

## 📥 API Usage

### Endpoint
```
POST /query
Content-Type: application/json
```

### Example Request
```json
{
  "question": "Should I use gpt-4o-mini which AI proxy supports, or gpt3.5 turbo?",
  "image": "<optional base64-encoded image>"
}
```

### Example Response
```json
{
  "answer": "You must use `gpt-3.5-turbo-0125`, even if the AI Proxy only supports `gpt-4o-mini`.",
  "links": [
    {
      "url": "https://discourse.onlinedegree.iitm.ac.in/t/ga5-question-8-clarification/155939/4",
      "text": "Use the model that’s mentioned in the question."
    }
  ]
}
```

---

## 🛠️ Local Setup

```bash
# Clone repo and enter folder
git clone https://github.com/anantsathe/project.git
cd project

# Create and activate virtual environment
python3 -m venv venv
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Set your API key in .env file
echo "API_KEY=Bearer YOUR_AIPIPE_KEY_HERE" > .env

# Run preprocessing script (only once)
python preprocess.py

# Run API locally
uvicorn api.app:app --host 0.0.0.0 --port 8000 --reload
```

---

## 📊 Evaluation with Promptfoo

To evaluate this API using the official test cases:

1. Update your YAML:
```yaml
providers:
  - id: https
    config:
      url: https://project-fcs4-pmr8aqs7h-anant-sathes-projects.vercel.app/query
```

2. Run:
```bash
npx -y promptfoo eval --config api/project-tds-virtual-ta-promptfoo.yaml
```

---

## ✅ Health Check

To verify deployment status:
```
GET /health
```

---

## 🧪 Bonus Points

✅ `preprocess.py` included to:
- Parse Discourse and course content  
- Chunk text  
- Generate embeddings  
- Populate SQLite knowledge base  

---

## 📜 License

This project is licensed under the [MIT License](./LICENSE).

---

## 👤 Author

**Anant S. Sathe**  
33+ years in cement operations, analytics & consulting  
Currently upskilling through IIT Madras' BSc in Data Science  
GitHub: [@anantsathe](https://github.com/anantsathe)

---