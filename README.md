# ResumeAI — Resume Analysis & Interview Prep

ResumeAI is a local Streamlit app that turns a text-based PDF resume into practical career insights: an ATS-style score, sample job matches, extracted skills, role predictions, skill-gap suggestions, and interview practice questions.

> **Important:** This is a learning and decision-support tool, not a hiring system or a guarantee of ATS results. Scores, role matches, salary ranges, and predictions are based on bundled rules and sample data; review them critically.

## Features

- **PDF parsing:** Extracts resume text, detects common sections, and looks for contact details.
- **ATS-style scoring:** Scores keyword optimization (25%), skills relevance (20%), structure (20%), experience (15%), education (10%), contact completeness (5%), and additional sections (5%), with feedback for each area.
- **Job matching:** Ranks eight example roles using TF-IDF similarity and overlap with listed required skills. Results include matched and missing skills and sample role information.
- **Skill analysis:** Identifies technical skills and groups them into categories such as programming languages, ML/AI, frameworks, databases, cloud/DevOps, and tools.
- **Skill-gap analysis:** Compares detected resume skills with a selected example role and suggests skills and certifications to explore.
- **Role prediction:** Compares resume text with bundled synthetic examples using Logistic Regression, Random Forest, or Naive Bayes; displays confidence and influential terms.
- **Interview preparation:** Builds technical, behavioral, role-specific, and scenario questions from the local question bank.
- **Interactive analytics:** Displays scores, matches, skills, and predictions in Plotly charts.
- **Demo mode:** Try the workflow with the included sample resume without uploading a file.

## Requirements

- Python 3.10 or later
- pip

The app uses Streamlit, scikit-learn, NumPy, pandas, PDF parsing libraries, and Plotly. See [requirements.txt](requirements.txt) for the dependency list.

## Run locally

### Windows PowerShell

```powershell
py -3.10 -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r requirements.txt
streamlit run app.py
```

If PowerShell blocks activation, you can invoke Streamlit directly after installing dependencies:

```powershell
.\.venv\Scripts\python.exe -m streamlit run app.py
```

### macOS / Linux

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install -r requirements.txt
streamlit run app.py
```

Streamlit prints a local URL (usually `http://localhost:8501`) when the app starts. Open it in your browser.

## Use the app

1. Open **Upload & Analyze** from the sidebar.
2. Upload a PDF resume or select **Load Sample Resume**.
3. Review the extracted text and detected details.
4. Select **Run Full AI Analysis**.
5. Explore the results in **ATS Score**, **Job Matches**, **Skill Analysis**, **Skill Gap**, **Role Predictor**, **Interview Prep**, and **Analytics Dashboard**.

Use **Start over** in the sidebar to clear the current analysis and begin again.

## Project layout

```text
.
├── app.py                         # Streamlit UI and analysis workflow
├── resume_parser.py               # PDF text extraction and section detection
├── skill_extractor.py             # Skill extraction and categorization
├── ats_calculator.py              # ATS-style score and feedback
├── recommender.py                 # Example-role matching and skill gaps
├── role_predictor.py              # Text-based role classification
├── interview_generator.py         # Interview question pack generation
├── dashboard.py                   # Plotly chart builders
├── config.py                      # Shared scoring and parsing configuration
├── datasets/
│   ├── job_descriptions.py        # Example roles, skills, and certifications
│   └── interview_questions.py     # Local interview question bank
└── requirements.txt               # Python dependencies
```

## Data, privacy, and limitations

- The app analyzes PDF text locally in the running Python process and keeps analysis results in Streamlit session state; it does not configure a database or user-account storage.
- The bundled role descriptions, salary ranges, certification suggestions, and role-prediction training examples are sample data—not live job listings or a professionally validated labor-market dataset.
- The role predictor trains from small, synthetic examples included in the source. Its confidence and displayed accuracy should not be treated as reliable real-world performance metrics.
- PDF extraction is text-based and limited to the first 20 pages and 50,000 characters. Scanned/image-only PDFs may not yield usable text because OCR is not configured.
- Resume formatting and wording can affect extraction and scores. The app does not determine whether a candidate is qualified, and an ATS score does not predict the behavior of any specific employer's system.
- If you run this app on a hosted or shared machine, consider who controls that environment before uploading a resume containing personal information.

## Troubleshooting

- **`streamlit` is not recognized:** Activate the virtual environment, or run Streamlit through the environment's Python as shown above.
- **PDF text is missing:** Try a text-based PDF rather than a scan, or load the sample resume to confirm the analysis flow works.
- **Dependency/import errors:** Confirm the intended Python interpreter is active, then install from `requirements.txt` again.

## License

No license is currently specified. Add a license file before redistributing this project if you want to grant others explicit reuse rights.
