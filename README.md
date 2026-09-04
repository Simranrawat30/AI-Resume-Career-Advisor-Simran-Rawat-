#  🚀AI-Resume-Career-Advisor-Simran-Rawat-


AI Resume & Career Advisor is an advanced AI-powered full-stack application designed to help students and job seekers align their resumes with specific Job Descriptions (JD). The system extracts text from PDF documents, indexes the job description using a Retrieval-Augmented Generation (RAG) vector database pipeline, compares candidate qualifications, and runs a career advisor agent layer to generate suitability reports, identify skill gaps, provide interview preparation roadmaps, and build a personalized 3-month learning roadmap.

# 🌟 Key Features

📄 Contextual PDF Parsing: Extracts unstructured data from resumes and job descriptions using pypdf.
🔍 Vector-Based RAG Retrieval: Implements text chunking and TF-IDF Cosine Similarity for targeted context extraction.
🤖 Multi-Agent Evaluation Pipeline:
Agent 1 (ATS Recruiter): Computes match percentage and audits missing technical capabilities.
Agent 2 (Career Coach): Generates targeted interview preparation questions and a week-by-week 3-month action plan.
📊 Interactive Dashboard: Modern dark-mode UI with compatibility meters, dual output tabs, and single-click Markdown report export.


# 📉SYSTEM ARCHITECTURE & DATA FLOW📈

Below is the architecture diagram showing how data flows from user input through the PDF parser, the RAG vector store, the Career Advisor Agent, and the Gemini LLM to the React dashboard.

       +--------------------------------------------------------+
       |                     User Interface                     |
       |  (React, Vite, Tailwind CSS, Recharts, Lucide Icons)   |
       +------------+-------------------------------+-----------+
                    |                               ^
        Upload Resume & JD PDFs              Render Analysis Report
                    |                               |
                    v                               |
       +------------+-------------------------------+-----------+
       |                     FastAPI Backend                    |
       |                   (main.py / Python)                   |
       +------------+-------------------------------+-----------+
                    |                               |
             PDF File Stream                 Structured JSON
                    |                               |
                    v                               |
       +------------+-------------+                 |
       |        PDF Parser        |                 |
       |         (PyPDF)          |                 v
       +------------+-------------+        +--------+----------+
                    |                      |  Career Advisor   |
              Cleaned Text                 |      Agent        |
                    |                      | (advisor_agent.py)|
                    v                      +--------+----------+
       +------------+-------------+                 |
       |   Text Chunking Engine   |                 | Orchestrate
       |   (Character Overlap)    |                 | Sub-prompts
       +------------+-------------+                 v
                    |                      +--------+----------+
              Text Chunks                  |    Gemini LLM     |
                    |                      | (gemini-1.5-flash)|
                    v                      +-------------------+
       +------------+-------------+
       |     Embedding Model      |
       |  (SentenceTransformers)  |
       +------------+-------------+
                    |
              Vector Embeddings
                    |
                    v
       +------------+-------------+
       |   ChromaDB Vector Store  |
       |     (Cosine Metric)      |
       +--------------------------+



Features (maps to assignment requirements)

Requirement	Implementation
Prompt Engineering — resume analysis	prompts/templates.py::RESUME_ANALYSIS_PROMPT
Prompt Engineering — skill gap identification	Same prompt; missing_skills / matched_skills fields
RAG — retrieve job descriptions from PDFs	utils/pdf_utils.py + rag/vector_store.py
Agent — resume reviewer	agents/resume_reviewer.py
Agent — career advisor	agents/career_advisor.py
Output — resume score	Tab 1 in app.py
Output — missing skills	Tab 1 in app.py
Output — interview prep roadmap	Tab 2 in app.py
Stretch — 3-month learning plan	Tab 3 in app.py (timeframe selectable: 1/3/6 months)
# 🎬 SETUP

pip install -r requirements.txt
cp .env.example .env
# edit .env and add your OPENAI_API_KEY

streamlit run app.py