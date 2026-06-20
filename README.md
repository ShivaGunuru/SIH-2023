# 🧠 Mental Health Self-Identification System

![Python](https://img.shields.io/badge/Python-3.9%2B-blue?logo=python&logoColor=white)
![Flask](https://img.shields.io/badge/Flask-2.x-black?logo=flask&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-orange?logo=scikitlearn&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-EC2-FF9900?logo=amazonaws&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-green)

> A machine learning-powered web application that enables individuals to self-assess their mental health status through lifestyle input data — built for Smart India Hackathon 2023.

---

## 📌 Table of Contents

- [About the Project](#about-the-project)
- [Key Features](#key-features)
- [Tech Stack](#tech-stack)
- [Folder Structure](#folder-structure)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Running Locally](#running-locally)
- [Model Details](#model-details)
- [Screenshots](#screenshots)
- [Deployment](#deployment)
- [About the Author](#about-the-author)

---

## About the Project

Mental health awareness remains critically underserved in India, with limited access to clinical assessments for most of the population. This project addresses that gap by providing an accessible, data-driven self-screening tool.

Users input lifestyle indicators (sleep, stress levels, screen time, mood, and more), and the system predicts their mental health status across five risk levels — from **Severe** to **Optimal** — using a trained Random Forest classifier with **87% accuracy** on a dataset of 10,000+ records.

Built as part of **Smart India Hackathon 2023**, this project combines ML research with a deployable Flask web interface, made accessible via AWS EC2.

---

## Key Features

- **5-Class Mental Health Classification** — Severe / Moderate / Mild / Good / Optimal
- **Real-time Predictions** — Instant results via a responsive web form
- **Trained on 10,000+ Records** — Robust dataset with thorough preprocessing and feature engineering
- **Dual Model Evaluation** — Logistic Regression vs. Random Forest compared; best model persisted via `pickle`
- **AWS EC2 Deployed** — Scalable cloud deployment for public accessibility
- **Lightweight Architecture** — Flask backend, no heavy dependencies

---

## Tech Stack

| Layer         | Technology                        |
|---------------|-----------------------------------|
| Language      | Python 3.9+                       |
| Web Framework | Flask                             |
| ML Library    | scikit-learn                      |
| Data          | Pandas, NumPy                     |
| Frontend      | HTML5, CSS3 (Jinja2 templates)    |
| Deployment    | AWS EC2                           |
| Model Storage | Pickle (`.pkl`)                   |

---

## Folder Structure

**Current structure** (as committed):

```
SIH-2023/
├── static/
│   └── CSS/
├── templates/
├── app.py
├── train.py
├── test.py
├── data.csv
├── model.pkl
└── README.md
```

**Recommended structure** (for clarity and scalability):

```
SIH-2023/
├── app/
│   ├── __init__.py
│   ├── routes.py              # Flask route handlers
│   └── predictor.py           # Model loading + prediction logic
│
├── data/
│   ├── raw/
│   │   └── data.csv           # Original dataset
│   └── processed/             # Cleaned/transformed data (gitignored)
│
├── model/
│   ├── train.py               # Model training script
│   ├── evaluate.py            # Evaluation metrics + comparison
│   └── artifacts/
│       └── model.pkl          # Serialized trained model
│
├── notebooks/
│   └── eda_and_modeling.ipynb # Exploratory analysis + experiments
│
├── static/
│   ├── css/
│   │   └── styles.css
│   └── assets/
│
├── templates/
│   ├── index.html             # Input form
│   └── results.html           # Prediction output
│
├── tests/
│   └── test_predictor.py      # Unit tests for prediction logic
│
├── .gitignore
├── requirements.txt
├── Procfile                   # For EC2/cloud deployment
├── run.py                     # App entry point
└── README.md
```

> Key changes: isolate model artifacts into `model/artifacts/`, move raw data to `data/raw/`, centralize Flask logic into an `app/` package, and add `tests/` for coverage.

---

## Getting Started

### Prerequisites

- Python 3.9 or higher
- pip
- (Optional) virtualenv or conda

### Installation

```bash
# 1. Clone the repository
git clone https://github.com/ShivaGunuru/SIH-2023.git
cd SIH-2023

# 2. Create and activate a virtual environment
python -m venv venv
source venv/bin/activate        # On Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt
```

> If `requirements.txt` is not present, install manually:
> ```bash
> pip install flask scikit-learn pandas numpy
> ```

### Running Locally

```bash
# Train the model first (if model.pkl is not already present)
python train.py

# Start the Flask server
python app.py
```

Open your browser at `http://127.0.0.1:5000`

---

## Model Details

### Input Features

| Feature              | Type    | Description                           |
|----------------------|---------|---------------------------------------|
| `Age`                | Float   | User's age                            |
| `Gender`             | Binary  | Male (1) / Female (0)                 |
| `ScreenTime`         | Float   | Daily screen time in hours            |
| `ActiveLifestyle`    | Float   | Physical activity score               |
| `SleepTime`          | Float   | Average sleep in hours                |
| `StressLevels`       | Float   | Self-reported stress (scale)          |
| `Mood`               | Float   | Daily mood score                      |
| `SocialRelationship` | Float   | Social engagement score               |

### Output Classes

| Class | Label     | Description                     |
|-------|-----------|---------------------------------|
| 0     | Severe    | Immediate attention recommended |
| 1     | Moderate  | Signs of significant distress   |
| 2     | Mild      | Minor concerns, monitor closely |
| 3     | Good      | Generally healthy mental state  |
| 4     | Optimal   | Excellent mental health          |

### Model Performance

| Model               | Accuracy  |
|---------------------|-----------|
| Logistic Regression | ~79%      |
| Random Forest       | **87%**   |

Random Forest selected and serialized to `model.pkl` for production use.

---

## Deployment

The application is deployed on **AWS EC2** for scalable public access.

```bash
# On EC2 instance
git clone https://github.com/ShivaGunuru/SIH-2023.git
cd SIH-2023
pip install -r requirements.txt
python app.py --host=0.0.0.0 --port=80
```

> Ensure port 80 (or 5000) is open in your EC2 Security Group inbound rules.

---

## About the Author

**Gunuru Venkata Shiva Kumar**
B.Tech CSE | GITAM University, Visakhapatnam (CGPA: 8.99)
Assistant System Engineer — Tata Consultancy Services

A backend-focused engineer with expertise in Java, Spring Boot microservices, and Python ML workflows. Experienced in building production-grade systems with REST APIs, cloud deployment, and data-driven applications.

- 📧 shiva.gunuru@gmail.com
- 🔗 [GitHub](https://github.com/ShivaGunuru)
- 🔗 [LinkedIn](https://linkedin.com/in/shiva-gunuru)

---

## License

This project is open-source under the [MIT License](LICENSE).

---

> *Built for Smart India Hackathon 2023 — contributing to accessible mental health awareness through technology.*
