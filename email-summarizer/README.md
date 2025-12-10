About this project:
- This project is a full end-to-end AI email workflow system that automates:
- Email ingestion (CSV + JSON parsing from real-world exports)
- Data cleaning & preprocessing
- Email categorization and prioritization
- Summarization of individual and grouped emails
- Generation of LLM-powered response drafts
- Evaluation of those responses using an LLM-as-a-judge framework
- Export of results and summaries as structured datasets
  
My project demonstrates practical applied generative AI, RAG-like preprocessing, complex data wrangling, and multi-step pipeline design.This project was built as part of an applied generative AI module,
but the architecture is fully generalizable to enterprise email triage, customer support automation, and workflow optimization systems

Features Worth Mentioning: 
Email Data Pipeline
- Reads emails from multiple raw formats (CSV and JSON)
- Normalizes inconsistent fields, handles malformed timestamps, and converts everything to UTC
- Groups emails by sender, category, and urgency
- Extracts critical/high-priority messages based on rule-based filters

My Workflow
- Generates clean summary descriptions of each email thread
- Uses chunking + abstraction prompts to handle long email bodies
- Produces human-readable dashboards of “yesterday’s emails”

LLM-Powered Response Generation
- Drafts appropriate replies tailored to each email’s content
- Supports different tones and styles
- Ensures responses include:
  - context
  - direct answers to sender questions
  - next steps
  - actionable details

LLM-as-a-Judge Evaluation
Uses a second LLM to evaluate the generated replies for:
- Relevance
- Clarity
- Actionability
- Strengths
- Areas for Improvement
- Overall Justification
- Outputs structured scoring results into CSVs.

Tech Stack
- Python
- pandas / NumPy
- OpenAI API (GPT-based summarization & evaluation)
- Datetime parsing utilities
- Custom helper functions for ingestion and cleaning
- Jupyter Notebook for development & testing

Architecure:
email-summarizer/
│
├── notebooks/
│      ├── MF2_Advanced_RAG.ipynb
│      └── GenAIModuleAssignment.ipynb
│
├── data/
│      ├── raw CSV/JSON email exports
│      └── structured intermediate files
│
├── outputs/
│      ├── critical_emails.csv
│      ├── yesterday_categorized.csv
│      ├── task2_gpt_responses_per_email.csv
│      ├── task3_llm_judge_evaluations.csv
│      └── summary dashboards
│
└── README.md  ← (this file)

How the System Works

Step 1: Load and Clean Email Data
- Normalizes timestamps
- Fixes inconsistent encodings
- Extracts fields (sender, subject, body, category, etc.)
- Removes malformed entries
- Sorts by most recent

Step 2: Identify Critical Emails
- Rule-based filtering detects emails that require immediate action:
e.g., approvals, urgent tasks, blockers, deadlines.

Step 3: Summaries via LLM
- Uses structured prompts to generate:
   - email-level summaries
   - category summaries
   - daily dashboard summaries

Step 4: Draft Responses via LLM
- For each critical email, the model generates:
   - a tailored reply
   - addressing questions
   - adding next-step instructions
   - enabling fast human-in-the-loop review

Step 5: Evaluate Responses
- A second LLM evaluates each generated reply, scoring:
   - relevance
   - clarity
   - actionability
   - justification

Results are exported for human review.

How to Run: 

Upload your own email dataset in CSV or JSON format to the data/ folder, then run the notebook:
notebooks/MF2_Advanced_RAG.ipynb

or to run locally: 
pip install -r requirements.txt
jupyter notebook

!!MAKE SURE TO SET YOUR OPENAI API KEY:
export OPENAI_API_KEY="your_key"

Future Improvements
- Add UI via Streamlit for interactive triage
- Implement sentiment scoring
- Add sender relationship lookup (internal vs external)
- Add RAG re-ranking for longer threads
- Deploy as a backend service with FastAPI
- Add human-in-the-loop editing interface
