# Ticket_Classifier
# Customer Support Ticket Classifier and Entity Extractor

This project builds a machine learning pipeline that classifies customer support tickets by:
- **Issue Type**
- **Urgency Level**

It also performs **entity extraction** to identify:
- Product names
- Dates
- Complaint related keywords

An interactive Gradio interface is provided for easy testing and demonstration.



##  Dataset

- File: `ai_dev_assignment_tickets_complex_1000.xls`
- Columns:
  - `ticket_id`
  - `ticket_text`
  - `issue_type` (Label)
  - `urgency_level` (Label)
  - `product` (Entity)

---

##  Pipeline Overview

### 1. **Preprocessing**
- Lowercasing, lemmatization, punctuation removal
- Missing value handling (drop or filled with `"Unknown"`)

### 2. **Feature Engineering**
- Bag-of-Words (BoW) for issue type classification
- TF-IDF for urgency level classification
- Additional features:
  - Character count
  - Word count
  - Sentiment score

### 3. **Model Training**
- Models evaluated: 
  - Logistic Regression
  - Random Forest
  - SVM
  - KNN
  - XGBoost

- **Selected Models**:
  - `KNeighborsClassifier` with **BoW** for `issue_type`
  - `KNeighborsClassifier` with **TF-IDF** for `urgency_level`
- Saved as:
  - `best_issue_model_knn_bow.pkl`
  - `best_urgency_model_knn_tfidf.pkl`

### 4. **Entity Extraction**
- Using spaCy's `en_core_web_sm`
- Extracts:
  - Product names (via `PhraseMatcher`)
  - Dates (NER)
  - Complaint keywords: `["broken", "late", "error", "delay", "damaged", "cancelled"]`



##  Gradio Interface

A Gradio web app is included to:
- Input ticket text
- Display predicted issue type and urgency level
- Show extracted entities (products, dates, complaint keywords)

### To Launch:

-bash
pip install -r requirements.txt
python ticket_classifier.py
