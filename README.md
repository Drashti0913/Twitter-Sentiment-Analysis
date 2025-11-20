# Twitter Sentiment Analysis — Drashti Bhavsar

**Personal project • Streamlit • Python • NLP • Deployed**

Live demo: https://twittersentimentanlyzerandvisualizer.streamlit.app/  

Original project report (source): `/mnt/data/Sentimental Analysis.pdf` (uploaded project report).  

---

## Executive summary
This repository contains a single-file Streamlit application that performs sentiment analysis on free-form text and Twitter data.  
It uses TextBlob for general text polarity/subjectivity and VADER for social-media-tuned sentiment on tweets. Tweets are collected without Twitter API using `snscrape`. The app produces interactive visualizations (pie/bar charts, token polarity bars) and a word cloud.

This version is presented as **my personal project** and has been polished for clarity, reproducibility, and interview conversations.

---

## Tech stack
- Python 3.8+  
- Streamlit (UI)  
- NLP: TextBlob, VaderSentiment  
- Data collection: snscrape (no official Twitter API required)  
- Visualization: Plotly, Matplotlib, WordCloud  
- Deployment example: Azure App Service (CI/CD via GitHub Actions)  
- Testing suggested: pytest (not included in single-file version)

---

## Key features
- Single text sentiment analysis with polarity & subjectivity (TextBlob)  
- Twitter sentiment analysis for a keyword (snscrape + VADER)  
- Token-level polarity scoring for quick insight into which words drive sentiment  
- Word cloud and interactive charts to explore results  
- Simple single-file deployable app (`app.py`) — easy to copy-paste and run

---

## Project files (single-file distribution)
This repository is distributed as a single Streamlit file for simplicity:

```
app.py       # Single-file Streamlit app containing scraping, preprocessing, sentiment, and visualizations
README.md
requirements.txt
```

---

## How it works (high-level)
1. **Input**: User types text or enters a keyword (for Twitter).  
2. **Fetch**: If Twitter search is chosen, `snscrape` pulls recent public tweets matching the keyword.  
3. **Preprocess**: Cleaning steps remove URLs, mentions, HTML entities, and non-alphanumeric noise; tokens and stopwords are handled.  
4. **Predict**: TextBlob is used for general text (polarity & subjectivity). VADER gives compound score for tweets, converted to labels (positive/neutral/negative).  
5. **Visualize**: Sentiment distribution (pie), time series (if scraped with dates), token polarity bar chart, and word cloud.  
6. **Deploy**: Streamlit serves the UI and can be deployed using Azure App Service (instructions below).

---

## Quick start — run locally

1. Clone (or create a new repo and paste `app.py` and this README):

```bash
git clone https://github.com/Drashti0913/Twitter-Sentiment-Analysis.git
cd Twitter-Sentiment-Analysis
```

2. Create a virtual environment & install:

```bash
python -m venv venv
# macOS / Linux
source venv/bin/activate
# Windows (PowerShell)
.\venv\Scripts\Activate.ps1

pip install -r requirements.txt
# If you don't have a requirements file, install manually:
# pip install streamlit pandas textblob vaderSentiment snscrape wordcloud plotly matplotlib nltk
python -m textblob.download_corpora   # ensures TextBlob corpora available
```

3. Run:

```bash
streamlit run app.py
```

---

## Requirements
Add to `requirements.txt`:

```
streamlit
pandas
textblob
vaderSentiment
snscrape
wordcloud
matplotlib
plotly
nltk
python-dotenv
```

(Exact pins are optional; the app was developed with Python 3.8+ and recent package versions.)

---

## UI design & improvements (this version)
- Slightly improved UI compared to the original: clearer headings, explanatory text, cached scraping, and responsive visualizations.
- Sidebar navigation includes: **Text Analysis**, **Twitter Analysis**, **About**.
- Token-level polarity bars help interviewers discuss implementation decisions and trade-offs.

---

## Deploying to Azure App Service (kept in README)
This project can be deployed to Azure App Service; high-level steps:

1. Create an Azure account and a resource group.
2. Create an App Service (Linux) and choose Python 3.8+ runtime.
3. Add a `requirements.txt` to the repo root and ensure `streamlit run app.py --server.port $PORT` is compatible with App Service. (Azure App Service may require an entrypoint via a `startup.txt` or `gunicorn` wrapper for web apps; for Streamlit Community or Streamlit for Teams, simply use Streamlit deploy methods.)
4. Configure CI/CD: connect GitHub repository to the App Service (Deployment Center) so pushes to `main` automatically deploy.
5. Ensure the machine has `snscrape` available; if scraping at scale or commercially, consider official API access and rate-limiting.

(For detailed step-by-step Azure instructions, follow Azure docs for Python web apps + your chosen deployment method. The app was previously deployed at the link above.)

---

## Ethics & Data Use
- This tool reads **public** tweets only (via scraping). Use responsibly: respect rate limits, robots.txt, and platform terms.
- Do not use scraped data for harassment, doxxing, or unauthorized profiling.

---

## What I learned (MLH-focused)
- Engineering: converting an exploratory demo into a single-file production-ready app that’s easy to run and discuss in interviews.  
- NLP: dealing with noisy social media text; combining lexicon-based approach (VADER) which is strong on social text, with TextBlob for general text.  
- Systems: deploying and CI/CD options (Azure) and working around Twitter API access changes using `snscrape`.  
- UX: communicating results via charts and token-level insights so interviewers can focus on design decisions and evaluation.

---

## Future improvements (recommended)
- Replace lexicon approach with a fine-tuned transformer (DistilBERT) to improve accuracy.  
- Add Dockerfile & production CI (lint/test/build).  
- Add multi-language support.  
- Add rate-limiting and respectful scraping logic for production.

---

## Contact
Drashti Bhavsar — drashtibhavsar09@gmail.com  
LinkedIn: https://www.linkedin.com/in/drashtibhavsar9/

---
