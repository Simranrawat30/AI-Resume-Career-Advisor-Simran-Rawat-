#  🚀AI-Resume-Career-Advisor-Simran-Rawat-


AI Resume & Career Advisor is an advanced AI-powered full-stack application designed to help students and job seekers align their resumes with specific Job Descriptions (JD). The system extracts text from PDF documents, indexes the job description using a Retrieval-Augmented Generation (RAG) vector database pipeline, compares candidate qualifications, and runs a career advisor agent layer to generate suitability reports, identify skill gaps, provide interview preparation roadmaps, and build a personalized 3-month learning roadmap.

# 🌟 KEY FETURES

   1•📄 Contextual PDF Parsing: Extracts unstructured data from resumes and job descriptions using pypdf.
   2•🔍 Vector-Based RAG Retrieval: Implements text chunking and TF-IDF Cosine Similarity for targeted context extraction.
   3•🤖 Multi-Agent Evaluation Pipeline:
          •Agent 1 (ATS Recruiter): Computes match percentage and audits missing technical capabilities.
          •Agent 2 (Career Coach): Generates targeted interview preparation questions and a week-by-week 3-month action plan.
   4•📊 Interactive Dashboard: Modern dark-mode UI with compatibility meters, dual output tabs, and single-click Markdown report export.


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




# 🎬 SETUP

pip install -r requirements.txt
cp .env.example .env
# edit .env and add your OPENAI_API_KEY

streamlit run app.py

# 📂 REPOSITORY SRUCTURE

Resume-Advisor-AI/
│
├── .env                       # API credentials (git-ignored)
├── .gitignore                 # Standard Python ignore rules
├── app.py                     # Streamlit frontend & RAG pipeline logic
├── requirements.txt           # Production dependencies
└── README.md                  # Comprehensive documentation
# 🚀 QUICKSTART GUIDE

 # 1. Clone the Repository
   git clone [https://github.com/iharshsinghh/Resume-Advisor-AI.git](https://github.com/iharshsinghh/Resume-Advisor-AI.git)
   cd Resume-Advisor-AI
 # 2. Set Up Virtual Environment
   python -m venv venv
   # Windows:
   venv\Scripts\activate
   # Linux/macOS:
   source venv/bin/activate
 # 3. Install Dependencies
   pip install -r requirements.txt
 # 4. Configure Environment Variables
   GOOGLE_API_KEY="your_gemini_api_key_here"
 # 5. Run the Application
   python -m streamlit run app.py --server.fileWatcherType none