# Unstructured Language Across Organizational Hierarchies

**Authors:** Desiree Bengalli, Andrea Guarnieri, Tancredi Liani, Andrea Lisci, Giada Poloni  
**Institution:** Bocconi University  
**Dataset:** Enron Email Corpus (Klimt & Yang, 2004)

---

## Overview

This project investigates how **language and communication patterns differ across hierarchical levels** within organizations, using the **Enron Email Dataset** as a case study.  
By combining linguistic, emotional, and semantic analysis, we uncover how executives, middle managers, and employees **express, react, and communicate differently**, especially during crisis periods.

Our approach integrates:
- **Data cleaning and preprocessing**  
- **Exploratory Data Analysis (EDA)**  
- **Hierarchical classification (SVM, XGBoost)**  
- **Sentiment analysis (RoBERTa, DistilBERT)**  
- **Topic modeling (LDA, BERTopic)**  

---

## Setup and Requirements

Download the **Enron Email Corpus**, as provided by Klimt & Yang (2004):
```text
https://www.cs.cmu.edu/~enron/
```

Update file paths in each notebook accordingly.

---

## 1. Data Cleaning

Notebook: `Cleaning.ipynb`

- Extracted fields: timestamp, sender, recipients, body  
- Filtered only trusted domains (`enron.com`, `outlook.com`, etc.)  
- Manually matched sender names to known Enron employees  
- Labeled employees by hierarchy:
  - 19 Executives  
  - 75 Middle Managers  
  - 97 Employees  
- Removed signatures, disclaimers, replies, and system-generated text

---

## 2. Exploratory Data Analysis (EDA)

Notebook: `EDA.ipynb`

- **Verbosity:** Executives write shorter, more direct emails  
- **Lexical focus:**  
  - Executives → coordination, crisis management  
  - Managers → project control and reporting  
  - Employees → task execution  
- **Lexical diversity:** Similar across levels (MTLD, MATTR)  
- **Named Entities:** Frequent mentions of FERC, PUC, DOE, etc.

---

## 3. Hierarchical Classification

Notebook: `Classification.ipynb`

Models:
- **Support Vector Machine (SVM)**
- **Gradient Boosting (XGBoost)**

Features:
- TF-IDF, number of recipients, email length  
- Time of day (night emails proxy for executives)  
- Presence of courteous/directive keywords (“please”, “order”, “crisis”)

| Model | Level | Recall |
|--------|--------|--------|
| SVM | High | 91% |
| SVM | Medium | 68% |
| SVM | Low | 54% |
| XGBoost | High | 90% |
| XGBoost | Medium | 67% |
| XGBoost | Low | 68% |

> Executives’ messages are the most distinctive due to consistent, directive language.

---

## 4. Sentiment Analysis

Notebook: `Sentiment.ipynb`

Used transformer models:
- `roberta-base`
- `distilbert-base-uncased`

Findings:
- Sentiment peaks in early 2000 (broadband expansion optimism)
- Sharp decline mid-2001 (Blockbuster deal collapse, crisis unfolding)
- Executives’ sentiment drops earlier and more sharply

---

## 5. Topic Modeling

### LDA (`LDA.ipynb`)
- Tuned parameters (α, η, k) via grid search  
- Limited interpretability — topics often generic (e.g., “meetings”, “workflow”)

### BERTopic (`BERTopic.ipynb`)
- Used transformer embeddings (`BAAI-llm`) + KMeans for stability  
- Improved coherence and semantic grouping  
- Identified crisis-related topics aligning with real Enron events (2000–2001 energy crisis)

| Level | Topics | Example Themes |
|--------|--------|----------------|
| Low | 15 | Operational reporting, energy variance |
| Medium | 8 | Transactions, coordination, informal chats |
| High | 12 | Market instability, executive meetings |

> Topics differ significantly across levels — almost no overlap.

---

## 6. Key Insights

- Hierarchical level shapes **how** and **what** people communicate.  
- **Executives** use directive, emotionally restrained language.  
- **Employees** focus on tasks and show stronger sentiment swings.  
- **Topic separation** reinforces that role defines both perspective and vocabulary.  
- **Crisis awareness** emerges earlier in executive communication.

---

## References

- Klimt, B., & Yang, Y. (2004). *The Enron Corpus.* CEAS Conference on Email and Anti-Spam.  
- Diesner, J. et al. (2005). *Communication networks from the Enron corpus.* Computational & Mathematical Organization Theory.  
- Belay, A. et al. (2024). *Sentiment analysis of Enron emails: Challenges in role-agnostic aggregation.* Journal of Applied NLP Research.  
- Thomas, C. W. (2002). *The Rise and Fall of Enron.* Journal of Accountancy.  
- Federal Energy Regulatory Commission (2005). *The Western Energy Crisis and the Enron Bankruptcy.*

---

