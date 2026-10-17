# Scam Shield

### Machine Learning Based Online Scam and Social Engineering Message Detection System

ScamShield is a web-based cybersecurity and machine learning project designed to detect potentially fraudulent, promotional, and legitimate messages.

The system uses natural language processing and supervised machine learning to analyze message content and classify it into three categories:

- **Normal** — regular legitimate messages
- **Promotional** — legitimate marketing or promotional messages
- **Scam / Smishing** — messages intended to deceive users, request sensitive information, create urgency, or direct users toward fraudulent activity

The project is designed as a practical application of machine learning to a real-world cybersecurity problem.

---

## Features

- Three-class message classification
- Bengali, English, Banglish, and code-mixed message support
- TF-IDF based text feature extraction
- Security-oriented feature extraction
- Multiple machine learning models
- Model performance comparison
- Accuracy, Precision, Recall and F1-score evaluation
- Confusion matrix visualization
- Prediction confidence
- Suspicious message indicators
- REST API using FastAPI
- React-based web interface
- Vercel frontend deployment
- Render backend deployment
- Zero-cost development and deployment approach

---

## Problem Statement

Online scams and social engineering attacks increasingly target ordinary users through SMS, messaging platforms, email, and other communication channels.

Attackers commonly use techniques such as:

- Urgency
- Fear
- Reward promises
- Financial pressure
- Fake account warnings
- Impersonation
- Credential requests
- Suspicious links

Many users may not recognize these patterns before interacting with a malicious message.

ScamShield attempts to address this problem by learning patterns from labeled message datasets and using machine learning to classify new messages.

---

## How It Works

```text
User Message
     |
     v
Text Preprocessing
     |
     v
Feature Extraction
     |
     +----------------------+
     |                      |
     v                      v
   TF-IDF            Security Features
     |                      |
     +----------+-----------+
                |
                v
          ML Classification
                |
       +--------+--------+
       |        |        |
       v        v        v
     Normal   Promo    Scam
                |
                v
       Security Indicators
                |
                v
          Web Interface
```

---

## Machine Learning Pipeline

The project follows a standard supervised machine learning workflow:

1. Data Collection
2. Data Exploration
3. Data Cleaning
4. Text Preprocessing
5. Feature Extraction
6. Train/Validation/Test Split
7. Model Training
8. Model Evaluation
9. Model Comparison
10. Best Model Selection
11. Model Serialization
12. Web API Integration
13. Prediction

---

## Dataset

### Primary Dataset

The primary dataset is the **Bengali SMS Smishing Dataset**.

It contains 7,005 SMS messages across three categories:

| Label | Description |
|---|---|
| `normal` | Regular benign messages |
| `promo` | Legitimate promotional messages |
| `smish` | Fraudulent or phishing SMS |

The dataset contains Bengali, English, Banglish, and code-mixed messages.

Dataset:

https://huggingface.co/datasets/shariul-islam/bengali-sms-smishing-dataset

### Dataset Split

| Split | Samples |
|---|---:|
| Training | 4,903 |
| Validation | 701 |
| Testing | 1,401 |
| Total | 7,005 |

### Secondary Dataset

The UCI SMS Spam Collection may be used as an external evaluation dataset to investigate how well the trained model generalizes to messages from another dataset.

Dataset:

https://archive.ics.uci.edu/dataset/228/sms

---

## Feature Engineering

ScamShield uses two major categories of features.

### Text Features

TF-IDF is used to transform message text into numerical feature vectors.

The system can use:

- Unigrams
- Bigrams
- Term frequency
- Inverse document frequency

### Security Features

Additional features can include:

- Message length
- Word count
- Digit count
- Special character count
- Uppercase ratio
- URL presence
- URL count
- Phone number presence
- Email presence
- Currency indicators
- OTP-related terms
- Account-related terms
- Login-related terms
- Password-related terms
- Urgency indicators
- Fear indicators
- Authority impersonation indicators
- Reward-related indicators
- Financial pressure indicators
- Credential-request indicators

These features provide additional information about common social-engineering patterns.

---

## Machine Learning Models

The project compares multiple supervised learning algorithms.

### 1. Multinomial Naive Bayes

Used as a strong baseline for text classification.

### 2. Logistic Regression

Used as an interpretable classification baseline and probability-based model.

### 3. Support Vector Machine

Used for classification with high-dimensional text features.

### 4. Random Forest

Used as an ensemble classification model.

### 5. Gradient Boosting

Used as an additional ensemble model for comparison.

The final production model will be selected based on validation and test performance rather than assuming one algorithm will always be the best.

---

## Evaluation Metrics

The models are evaluated using:

- Accuracy
- Precision
- Recall
- F1-score
- Confusion Matrix
- ROC-AUC where applicable

For ScamShield, particular attention is given to the recall and F1-score of the scam class because failing to identify a scam message can be more serious than incorrectly flagging a legitimate message.

---

## Web Application

The application contains several main sections.

### Home

Introduces ScamShield and its purpose.

### Analyze Message

Users can paste a message and request an analysis.

Example:

```text
Your account will be suspended today.
Verify your information immediately.
```

The system returns a classification and supporting indicators.

### Analysis Result

Example output structure:

```text
Prediction:
SCAM / SMISHING

Confidence:
94.7%

Detected Indicators:
- Urgency
- Account-related request
- Verification request
- Financial language
```

Actual prediction values depend on the trained model.

### Model Performance

Displays model comparison and evaluation results.

### About

Explains the machine learning workflow and project architecture.

---

## API

The backend is implemented using FastAPI.

### Health Check

```http
GET /api/health
```

### Analyze Message

```http
POST /api/analyze
```

Request:

```json
{
  "message": "Your account will be suspended. Verify immediately."
}
```

Example response:

```json
{
  "prediction": "smish",
  "confidence": 0.947,
  "risk_level": "high",
  "indicators": [
    "Urgency detected",
    "Account-related language detected",
    "Verification request detected"
  ]
}
```

### Model Information

```http
GET /api/model-info
```

---

## Technology Stack

### Frontend

- React
- Vite
- Tailwind CSS
- Axios
- Recharts

### Backend

- Python
- FastAPI
- Uvicorn
- Pydantic

### Machine Learning

- Scikit-learn
- Pandas
- NumPy
- Joblib

### NLP

- TF-IDF
- Text preprocessing
- N-gram features

### Visualization

- Matplotlib
- Seaborn
- Recharts

### Deployment

- Vercel
- Render

---

## Project Structure

```text
scamshield/
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── services/
│   │   └── App.jsx
│   ├── package.json
│   └── vite.config.js
│
├── backend/
│   ├── app/
│   │   ├── main.py
│   │   ├── api/
│   │   │   └── routes.py
│   │   ├── ml/
│   │   │   ├── predictor.py
│   │   │   ├── preprocessing.py
│   │   │   └── features.py
│   │   └── schemas/
│   │       └── request.py
│   │
│   ├── models/
│   │   ├── model.pkl
│   │   └── vectorizer.pkl
│   │
│   ├── requirements.txt
│   └── Dockerfile
│
├── data/
│   └── README.md
│
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_preprocessing.ipynb
│   ├── 03_model_training.ipynb
│   └── 04_model_comparison.ipynb
│
├── README.md
└── .gitignore
```

---

## Deployment Architecture

```text
                 User
                  |
                  v
        React Frontend
             Vercel
                  |
               HTTPS
                  |
                  v
          FastAPI Backend
              Render
                  |
          +-------+-------+
          |               |
          v               v
     Preprocessing     ML Model
          |               |
          +-------+-------+
                  |
                  v
             Prediction
                  |
                  v
            Web Response
```

---

## Development Plan

The project is planned for approximately two months with around one hour of development per day.

### Phase 1 — Dataset and Research

- Define problem
- Study dataset
- Explore class distribution
- Inspect message patterns
- Prepare project repository

### Phase 2 — Preprocessing

- Clean data
- Remove duplicates
- Normalize text
- Prepare training, validation and testing data

### Phase 3 — Feature Engineering

- Implement TF-IDF
- Implement n-gram features
- Extract security-related features

### Phase 4 — Model Development

- Train Naive Bayes
- Train Logistic Regression
- Train SVM
- Train Random Forest
- Train Gradient Boosting

### Phase 5 — Evaluation

- Compare models
- Generate confusion matrices
- Calculate classification metrics
- Select the best model
- Perform external evaluation where possible

### Phase 6 — Backend

- Build FastAPI application
- Load trained model
- Create prediction endpoint
- Create health endpoint
- Create model information endpoint

### Phase 7 — Frontend

- Build React interface
- Create message analysis page
- Create results page
- Create model performance page
- Connect frontend to backend

### Phase 8 — Deployment

- Deploy frontend to Vercel
- Deploy backend to Render
- Configure CORS
- Test production API
- Fix deployment issues

---

## Project Goals

The main goals of ScamShield are:

1. Apply machine learning to a practical cybersecurity problem.
2. Detect scam and social-engineering messages.
3. Compare multiple machine learning algorithms.
4. Investigate the effectiveness of text and security-related features.
5. Build a usable web-based detection interface.
6. Evaluate the model using multiple classification metrics.
7. Deploy the complete application using free hosting services.

---

## Limitations

ScamShield is a machine learning research and educational project.

It should not be considered a guaranteed security system.

A message classified as legitimate may still be malicious, and a legitimate message may occasionally be flagged as suspicious.

Model performance depends on the quality, language distribution, and characteristics of the training data.

The system does not directly access private SMS, WhatsApp, banking, or social-media accounts.

---

## Future Improvements

Possible future improvements include:

- Larger multilingual datasets
- Bengali-specific NLP improvements
- Real-time browser integration
- Mobile application
- Email integration
- URL reputation analysis
- Explainable AI techniques
- Transformer-based NLP models
- Continual learning
- Local/on-device inference
- Browser extension integration

---

## Ethical Considerations

ScamShield is intended for defensive cybersecurity and educational purposes.

The system should be used to help users identify potentially suspicious communication and should not be treated as a replacement for human judgment.

No private user messages should be collected or stored without appropriate consent.

---

## License

This project is developed for educational and research purposes.

Dataset licenses and attribution requirements should be followed separately according to the respective dataset providers.

---

## Author

**Ziham Mahmud**

CSE Undergraduate  


Interests:

- Cybersecurity
- Penetration Testing
- Machine Learning
- Artificial Inteligence
- Software Development

---

## Status

🚧 **Currently under development**

The final model performance, screenshots, live deployment links, and experimental results will be added after implementation and evaluation.
