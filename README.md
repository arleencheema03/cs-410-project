# Press Release vs. News Coverage: A TF-IDF/BM25 Framing Analysis

CS410 Fall 2026 Course Project

## Team

| Name | NetID | Role |
|------|-------|------|
| Arleen Cheema | arleenc2 | Project Coordinator |
| Sreenidhi Kannan | kannan6 | |

## Problem Statement

Journalists often base coverage heavily on official press releases (corporate, government, or institutional), but readers have no easy way to see how much of a news story's language is inherited directly from the source material versus independently reported or analyzed. Manually comparing a press release against resulting coverage across outlets is tedious and rarely done at scale, so this kind of "press release dependency" mostly goes unmeasured — even though it matters for understanding how much added value or independent framing news coverage actually provides.

## What This Project Does

This tool scrapes press releases alongside the news articles they generate across multiple outlets, then uses TF-IDF and BM25-based term weighting — implemented from scratch — to measure:

- **Overlap**: how much of a press release's language and emphasis carries over into each outlet's coverage
- **Divergence**: which terms each outlet introduces independently — its own framing, analysis, or context not present in the original release

Results are evaluated through case studies on specific press-release-driven stories (e.g., corporate earnings announcements, policy rollouts, product launches).

## Table of Contents

- [Installation](#installation)
- [Usage](#usage)
- [Architecture](#architecture)
- [Implementation Details](#implementation-details)
- [Case Studies](#case-studies)
- [Limitations](#limitations)
- [Repository Structure](#repository-structure)

## Installation

```bash
git clone https://github.com/[your-org]/[repo-name].git
cd [repo-name]
pip install -r requirements.txt
```

**Requirements:**
- Python 3.13
- [list key libraries once finalized, e.g., requests, beautifulsoup4, trafilatura, nltk/spacy, flask/streamlit]

## Usage

### 1. Scrape data

```bash
python scrape_releases.py --source [source] --output data/releases/
python scrape_articles.py --source [outlet] --output data/articles/
```

### 2. Build the index

```bash
python build_index.py --input data/ --output index/
```

### 3. Run the differential analysis

```bash
python analyze.py --release [release_id] --output results/
```

### 4. Launch the comparison viewer

```bash
python app.py
```

Then open `http://localhost:[port]` to view the side-by-side comparison interface.

*(Update commands/flags above to match your actual scripts as you build them.)*

## Architecture

```
[Press Releases]        [News Articles]
       |                       |
       v                       v
  [Scraper Modules] --------->  [Preprocessing: tokenize, stopwords, stemming]
                                        |
                                        v
                          [Inverted Index / Document Store]
                                        |
                                        v
                        [TF-IDF + BM25 Scoring Engine]
                                        |
                                        v
                    [Differential Analysis: Overlap & Divergence]
                                        |
                                        v
                       [Comparison Viewer / Case Study Output]
```

## Implementation Details

### Text Preprocessing
- [Describe tokenization, stopword removal, stemming/lemmatization choices]

### TF-IDF
- [Describe your TF-IDF formula, smoothing approach, vectorization]

### BM25
- [Describe your BM25 formula and parameter choices — k1 and b values used, and why]

### Differential Analysis
- **Overlap score**: [describe method — e.g., fraction of article's high-weight terms also high-weight in the release, or cosine similarity between release/article vectors]
- **Divergence terms**: [describe method — e.g., log-odds ratio or delta-weight comparison to surface terms high in the article but low/absent in the release]

## Case Studies

| # | Event | Press Release Source | Outlets Compared | Key Finding |
|---|-------|----------------------|-------------------|-------------|
| 1 | [e.g., Company X earnings report] | [source] | [outlet A, B, C] | [1-2 sentence summary] |
| 2 | | | | |
| 3 | | | | |
| 4 | | | | |

*(Full write-ups for each case study can live in `/case_studies/` with supporting output/screenshots.)*

## Limitations

- Corpus size: [note scale — number of release/article pairs analyzed]
- Event matching: [note whether matching was manual/curated vs. automated, and what that implies]
- Outlet selection: [note which outlets were included and any resulting selection bias]
- Scope: this tool measures lexical overlap and divergence — it does not make claims about journalistic quality, accuracy, or bias; divergence could reflect valuable added reporting or unrelated stylistic differences

## Repository Structure

```
.
├── README.md
├── requirements.txt
├── scrape_releases.py
├── scrape_articles.py
├── preprocessing.py
├── tfidf.py
├── bm25.py
├── analyze.py
├── app.py
├── data/
│   ├── releases/
│   └── articles/
├── case_studies/
└── tests/
```
