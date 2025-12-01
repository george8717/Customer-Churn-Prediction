📘 Customer Churn Prediction — ML Model + Flask Web App

This project predicts whether a telecom customer is likely to churn (leave the service).
It combines a machine learning model with a simple web interface, allowing users to input customer details and instantly see churn predictions.

The goal is to provide a complete, working end-to-end ML solution — from data preprocessing and model training to deployment through a Flask application.

🔍 What This Project Does

Loads and preprocesses the Telco Customer Churn dataset

Trains a machine learning model (Logistic Regression / RandomForest / XGBoost)

Saves preprocessing artifacts (encoders, scalers, feature order)

Provides a Flask-based web app where users can enter customer info

Predicts:

Churn (Yes/No)

Probability score

Essentially, it shows how to build and deploy a real ML model in a production-like workflow.

🛠️ Tech Stack Used
Machine Learning

Python

pandas — data cleaning & preprocessing

NumPy — numerical operations

scikit-learn — encoding, scaling, model training, evaluation

XGBoost (optional) — improved accuracy

joblib — saving ML artifacts

Backend / Deployment

Flask — lightweight web framework to serve predictions

HTML (Jinja templates) — form-based user interface

Environment / Tools

Virtual Environment (venv)

JSON for API requests

GitHub for version control


