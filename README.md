# AI Resume Parser & Matcher 🤖📄

An automated, intelligent recruitment pipeline built with **Python**, **Pydantic**, **Groq LLM**, and document-parsing libraries to automatically extract, evaluate, match, and rank candidate resumes against specific job descriptions.

---

## 🏗️ Architecture Flow Diagram

```mermaid
graph TD
    subgraph Input Phase
        A[Job Description Text] -->|LLM & Pydantic Extraction| B[Structured Job Object]
        C[Resumes Folder: PDF / DOCX] -->|File Readers: PyPDF & python-docx| D[Raw Resume Text]
    end

    subgraph Processing Phase
        D -->|LLM Call 1: parse_resume| E[Structured Resume Pydantic Object]
        B --> F[Job Requirements]
        E --> F
        F -->|LLM Call 2: final_score| G[Match Score & Evaluation Details]
    end

    subgraph Output Phase
        G --> H[Store in Results List]
        H -->|Sort by Score Descending| I[Top 2 Candidates]
        H -->|Sort by Score Descending| J[Lowest 2 Candidates]
    end

## ⚙️ Step-by-Step Workflow

1. **Step 1 (Job Description Initialization):** Defines the target role description, responsibilities, and technical requirements as raw text.
2. **Step 2 (Job Structuring via Pydantic):** Sends the JD through the Groq LLM using a strict JSON schema (`JobD`) to extract structured keys like role, required skills, preferred skills, and minimum experience.
3. **Step 3 (File Ingestion):** Automatically scans the local `resumes/` folder, checking file extensions and routing files to the appropriate reader (`pypdf` for `.pdf` files, `python-docx` for `.docx` files).
4. **Step 4 (Resume Parsing):** Extracts candidate information contextually (handling varying section names like "Work History", "Internships", etc.) and maps it into a clean `Resume` Pydantic model.
5. **Step 5 (Comparative Evaluation):** Sends both the structured job profile and the candidate profile to the LLM to calculate a precise matching score, identify gaps, provide interview tips, and give a final verdict (`MatchResult`).
6. **Step 6 (Ranking & Aggregation):** Sorts all evaluated candidates in descending order by their match score and prints out the **Top 2** and **Lowest 2** candidates.

---

## 📦 Tech Stack & Packages Used

* **[Groq API](https://console.groq.com)** (`llama-3.3-70b-versatile`) – High-speed LLM inference engine powering the extraction and evaluation steps.
* **[Pydantic](https://www.google.com/search?q=https://docs.pydantic.dev/)** – Enforces strict runtime data validation and generates JSON schemas for structured LLM outputs.
* **[pypdf](https://pypdf.readthedocs.io/)** – Extracts textual data layer from candidate PDF resumes.
* **[python-docx](https://python-docx.readthedocs.io/)** – Parses paragraphs and tables from Microsoft Word (`.docx`) resumes.
* **[python-dotenv](https://github.com/theskumar/python-dotenv)** – Securely loads environment variables (like `GROQ_API_KEY`) from a local `.env` file.
* **Built-in Python Modules** – `pathlib` for cross-platform directory handling and `json` for data serialization.

---

## 🚀 Getting Started

### Prerequisites

* Python 3.10+ installed on your system.
* [uv](https://www.google.com/search?q=https://github.5com/astral-sh/uv) (recommended) or standard `pip`.
* A free [Groq API Key](https://console.groq.com/).

### Installation & Setup

1. **Clone or download the repository**, and navigate to your project folder.
2. **Create a virtual environment and install dependencies**:
```bash
uv venv
# Activate virtual environment (Windows):
.venv\Scripts\activate

# Install required packages
uv pip install groq pydantic pypdf python-docx python-dotenv

```


*(If you run into any compatibility errors with docx, ensure you use `python-docx` and not the legacy `docx` library).*
3. **Set up your environment variables**:
Create a `.env` file in the root directory and add your Groq API key:
```env
GROQ_API_KEY=your_actual_groq_api_key_here

```


4. **Organize your workspace**:
Create a folder named `resumes` in the same directory as your script and drop your candidate files (`.pdf` or `.docx`) inside it.
5. **Run the script**:
```bash
python resume_parser.py

```



---

## 📂 Project Structure

```text
ai_engineer_map/
│
├── .env                # API Keys configuration (keep secret)
├── .gitignore          # Git exclusion rules (ignores /resumes and .venv)
├── resume_parser.py    # Main execution script
└── resumes/            # Folder containing candidate .pdf / .docx files
    ├── candidate_1.pdf
    └── candidate_2.docx

```

```

```
