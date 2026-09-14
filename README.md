# ResumeIQ — ATS Resume Analyzer & Optimizer

A production-quality ATS simulation system that analyzes resumes against job descriptions using a multi-factor NLP pipeline — similar to how enterprise ATS systems at top companies work.

<p align="center">
  <a href="https://ats-resume-analyser-yyc4.onrender.com/analyzer">
    <strong>🌐 Try ResumeIQ Live →</strong>
  </a>
</p>

> ⚠️ **Note:** The application is hosted on Render's free tier. The service may sleep after periods of inactivity, so the first request can take around 40–50 seconds while the service wakes up.

[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy?repo=https://github.com/Santosh-Mutyala-01/ATS_RESUME_ANALYSER)

---

## 📸 Preview

<p align="center">
  <img src="Screenshot%202026-05-07%20135719.png" alt="ResumeIQ ATS Analyzer Dashboard" width="900">
</p>

---

## 🚀 Quick Start

### 1. Clone the repository

```bash
git clone https://github.com/Santosh-Mutyala-01/ATS_RESUME_ANALYSER.git
cd ATS_RESUME_ANALYSER
```

### 2. Setup

#### Automatic Setup

```bash
chmod +x setup.sh
./setup.sh
```

#### Manual Setup

Create a virtual environment:

```bash
python3 -m venv venv
```

Activate it:

**macOS / Linux**

```bash
source venv/bin/activate
```

**Windows**

```bash
venv\Scripts\activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Download the spaCy language model:

```bash
python -m spacy download en_core_web_sm
```

### 3. Run the Application

```bash
python app.py
```

Open:

```text
http://localhost:5000
```

The application starts with the project introduction page.

Click **Get Started** to access the analyzer at:

```text
/analyzer
```

---

## 🌐 Live Demo

**[Open ResumeIQ →](https://ats-resume-analyser-yyc4.onrender.com/analyzer)**

The deployed application can be accessed directly from a browser without setting up the project locally.

> **Render Free Tier:** If the application has been inactive for a while, the service may sleep. The first request can therefore take approximately 40–50 seconds to load.

---

## ☁️ Deployment — Render

This project includes a `render.yaml` configuration for deployment on Render.

### One-Click Deployment

[![Deploy to Render](https://render.com/images/deploy-to-render-button.svg)](https://render.com/deploy?repo=https://github.com/Santosh-Mutyala-01/ATS_RESUME_ANALYSER)

### Manual Deployment

1. Open Render.
2. Select **New → Blueprint**.
3. Connect your GitHub account.
4. Select this repository.
5. Deploy using the included `render.yaml` configuration.

### GitHub Repository

[**ATS_RESUME_ANALYSER**](https://github.com/Santosh-Mutyala-01/ATS_RESUME_ANALYSER)

---

## 🧠 How It Works

ResumeIQ analyzes a resume against a job description using four major factors:

| Factor | Weight | Method |
|---|---:|---|
| **Keyword Match** | 30% | Exact + fuzzy matching using `SequenceMatcher` |
| **Semantic Similarity** | 30% | Sentence Transformer embeddings + cosine similarity |
| **Skill Coverage** | 20% | Taxonomy-based skill matching |
| **Experience Relevance** | 20% | Action verbs, quantification, and JD keyword relevance |

### Final ATS Score

The final ATS score is calculated as a weighted average of the four scoring components.

The scoring system also uses realism caps to avoid automatically producing unrealistically high scores.

A strong score therefore requires a resume to perform well across multiple dimensions rather than simply containing a large number of keywords.

---

## ✨ Features

### 📊 ATS Match Score

- Circular ATS score visualization
- Overall resume-to-job-description match score
- Individual score breakdown

### 📈 Match Analysis

- Radar chart across four scoring dimensions
- Keyword match analysis
- Semantic similarity
- Skill coverage
- Experience relevance

### 🔎 Keyword Analysis

- Keyword density analysis
- Low / optimal / high keyword indicators
- Relevant keyword identification
- Context-aware keyword suggestions

### 🧩 Skill Gap Analysis

- Identifies missing skills
- Ranks missing skills based on estimated impact
- Groups skills into categories
- Shows potential score improvement

### 📄 Resume Section Analysis

Detects missing or potentially weak resume sections and provides recommendations for improvement.

### ✍️ Resume Optimization

- Resume bullet-point improvement suggestions
- Stronger action-verb recommendations
- Context-aware sentence suggestions
- ATS optimization action plan

### 🗂️ Skill Clustering

Skills are organized into categories such as:

- Tools
- Techniques
- Soft Skills
- Domain Skills
- Programming Languages

### 👀 Resume Preview

Matched keywords can be highlighted directly in the resume preview for easier inspection.

---

## 🔄 Analysis Pipeline

```text
Resume PDF
    │
    ▼
PDF Text Extraction
    │
    ▼
Text Processing
    │
    ├───────────────┐
    ▼               ▼
Keyword Analysis   Skill Analysis
    │               │
    └───────┬───────┘
            ▼
    Semantic Similarity
            │
            ▼
    Experience Analysis
            │
            ▼
      Scoring Engine
            │
            ▼
    ┌───────────────────┐
    │    ATS Score      │
    │    Skill Gaps     │
    │    Keywords       │
    │    Section Health │
    │    Suggestions    │
    └───────────────────┘
            │
            ▼
    Interactive Dashboard
```

---

## 🏗️ Project Structure

```text
ATS_RESUME_ANALYSER/
│
├── app.py
├── requirements.txt
├── setup.sh
├── Dockerfile
├── render.yaml
├── ATS Analyzer.spec
│
├── utils/
│   ├── __init__.py
│   ├── text_extractor.py
│   ├── nlp_pipeline.py
│   ├── scoring_engine.py
│   ├── skill_analyzer.py
│   └── optimizer.py
│
├── templates/
│   └── index.html
│
├── static/
│   ├── css/
│   │   └── style.css
│   └── js/
│       └── app.js
│
├── dummy.pdf
├── test_resume.pdf
│
└── README.md
```

### Core Components

| File | Purpose |
|---|---|
| `app.py` | Flask application and API routes |
| `text_extractor.py` | Extracts text from uploaded PDF resumes |
| `nlp_pipeline.py` | NLP processing, phrase extraction, embeddings, and skill taxonomy |
| `scoring_engine.py` | Calculates the multi-factor ATS score |
| `skill_analyzer.py` | Skill matching, clustering, and skill-gap analysis |
| `optimizer.py` | Resume optimization suggestions |
| `index.html` | Main application interface |
| `app.js` | Frontend logic and dashboard interactions |
| `style.css` | Application styling |

---

## ⚙️ Tech Stack

| Layer | Technology |
|---|---|
| **Backend** | Flask 3.0 |
| **PDF Parsing** | pdfminer.six + pypdf |
| **NLP** | spaCy + `en_core_web_sm` |
| **Embeddings** | Sentence Transformers (`all-MiniLM-L6-v2`) |
| **Similarity** | scikit-learn cosine similarity + `SequenceMatcher` |
| **Frontend** | HTML + Tailwind CSS + Vanilla JavaScript |
| **Charts** | Chart.js 4.4 |
| **Fonts** | Syne + DM Sans |
| **Deployment** | Render |
| **Production Server** | Gunicorn |
| **Containerization** | Docker |

---

## 🔧 Configuration

Several parts of the analysis system can be customized.

### Skill Taxonomy

Edit:

```text
utils/nlp_pipeline.py
```

The `SKILL_TAXONOMY` configuration can be expanded with additional domain-specific skills.

### Skill Importance

Edit:

```text
utils/skill_analyzer.py
```

The `SKILL_IMPORTANCE` configuration controls skill weighting and estimated impact.

### Scoring Weights

Edit:

```text
utils/scoring_engine.py
```

The `WEIGHTS` configuration controls the contribution of the major scoring factors.

---

## 📝 Notes & Limitations

### PDF Support

The current implementation supports **text-based PDF resumes**.

Scanned or image-only PDFs require OCR, which is not currently included.

### First Startup

The first startup may take longer because the Sentence Transformer model needs to be downloaded.

The model used is:

```text
all-MiniLM-L6-v2
```

### Local Processing

Resume analysis is performed locally within the application and the current implementation does not send resume content to external APIs.

### ATS Score Interpretation

The score produced by ResumeIQ is an **ATS-style analytical estimate**, not an exact representation of the proprietary scoring system used by a specific company's ATS.

Different applicant tracking systems can use different parsing, ranking, and filtering methods.

---

## 🚀 Production Deployment

For production-style execution, the Flask application can be served using Gunicorn:

```bash
gunicorn app:app -w 4 -b 0.0.0.0:5000
```

The repository also includes:

- `Dockerfile`
- `render.yaml`

for deployment and containerization.

---

## 🛠️ Future Improvements

Potential improvements include:

- OCR support for scanned resumes
- Expanded skill taxonomy
- Domain-specific scoring
- Additional resume formats
- Improved job-description parsing
- Resume version comparison
- More advanced optimization recommendations
- Automated resume generation
- Larger evaluation datasets
- User accounts and saved analyses
- Additional deployment monitoring

---

## 📄 License

This project is licensed under the **MIT License**.

You are free to use, modify, and distribute the project according to the terms of the license.

---

## 👨‍💻 Author

### Santosh Mutyala

**Data Science | Machine Learning | AI**

- GitHub: [Santosh-Mutyala-01](https://github.com/Santosh-Mutyala-01)
- Project: [ATS Resume Analyzer](https://github.com/Santosh-Mutyala-01/ATS_RESUME_ANALYSER)
- Live Demo: [ResumeIQ](https://ats-resume-analyser-yyc4.onrender.com/analyzer)

---

## 🔗 Project Links

| Resource | Link |
|---|---|
| 🌐 **Live Demo** | [ResumeIQ](https://ats-resume-analyser-yyc4.onrender.com/analyzer) |
| 💻 **GitHub** | [ATS_RESUME_ANALYSER](https://github.com/Santosh-Mutyala-01/ATS_RESUME_ANALYSER) |
| ☁️ **Deploy to Render** | [Deploy](https://render.com/deploy?repo=https://github.com/Santosh-Mutyala-01/ATS_RESUME_ANALYSER) |

---

## ⭐ Support

If you find ResumeIQ useful, consider giving the repository a ⭐ on GitHub.
