📘 Customer Churn Prediction — Machine Learning + Flask App
🔍 What This Project Does

This project predicts whether a Telco customer is likely to churn (i.e., leave the service).
It provides a complete ML workflow — data preprocessing, model training, evaluation, artifact saving — and a simple Flask web application to make real-time churn predictions from user input.

This makes it a perfect end-to-end ML deployment mini-project.

📁 Project Structure
.
├── app.py
├── customer_churn_prediction.py
├── WA_Fn-UseC_-Telco-Customer-Churn.csv
├── input.txt
├── templates/
│   └── index.html
└── requirements.txt

🧩 Component Breakdown (Explained Clearly)
1. app.py — The Web Application

Entry point for the Flask app.

Loads saved model + preprocessing artifacts.

Renders the UI (templates/index.html).

Accepts form/JSON input and returns predictions.

Converts input into the same processed format used during training.

2. customer_churn_prediction.py — Model Training Script

This script:

Loads the Telco dataset

Cleans data (missing values, type conversions)

Encodes categorical features

Scales numeric features

Splits train/test

Trains a classifier (Logistic Regression / RandomForest / XGBoost)

Evaluates performance

Saves artifacts (model, encoder/scaler, feature order)

3. WA_Fn-UseC_-Telco-Customer-Churn.csv — Dataset

A popular public dataset containing:

Customer demographic info

Account details

Services subscribed

Monthly/total charges

Binary churn label

4. templates/index.html — Web Interface

Simple HTML form that:

Accepts all required customer inputs

Sends request to /predict

Displays churn prediction results

5. input.txt — Example Input (Optional)

Useful for quick testing via scripts or API calls.

6. requirements.txt

Lists all necessary Python packages (Flask, pandas, scikit-learn, joblib, etc.).

⚙️ Setup Instructions
1. Create and activate a virtual environment
Windows PowerShell
python -m venv venv
.\venv\Scripts\Activate.ps1

macOS / Linux
python3 -m venv venv
source venv/bin/activate

2. Install dependencies
pip install -r requirements.txt

3. Train the model (generate artifacts)

Run:

python customer_churn_prediction.py


This will:

Preprocess the raw dataset

Train an ML model

Evaluate metrics

Save:

model.joblib

preprocessor.joblib (or encoder/scaler)

features.json (feature order)

4. Run the Flask web app
python app.py


Then open:
👉 http://127.0.0.1:5000/

You will see the churn prediction form.

🌐 Example API Request (JSON)
curl -X POST http://127.0.0.1:5000/predict \
  -H "Content-Type: application/json" \
  -d '{
    "gender": "Male",
    "SeniorCitizen": 0,
    "Partner": "Yes",
    "Dependents": "No",
    "tenure": 12,
    "PhoneService": "Yes",
    "InternetService": "DSL",
    "Contract": "Month-to-month",
    "MonthlyCharges": 70.5,
    "TotalCharges": 700.0
  }'


Example response:

{
  "prediction": "Yes",
  "probability": 0.82
}

🧠 What Happens Internally (Quick ML Flow)
1. Data Cleaning

Convert TotalCharges to numeric

Fill/drop missing rows

Convert categories like Yes/No → 1/0

2. Preprocessing

One-hot encode categorical vars

Scale numeric vars (tenure, MonthlyCharges, TotalCharges)

3. Model Training

Typical models used:

Logistic Regression (baseline)

RandomForestClassifier

XGBoost (high accuracy)

4. Evaluation

Metrics printed:

Accuracy

Precision

Recall

F1-score

ROC AUC

5. Saving Artifacts

Using joblib.dump():

model

encoders/scalers

ordered feature list

💡 Inside app.py: Prediction Flow

Load model + preprocessing objects

Receive input from user

Build DataFrame with correct columns

Apply preprocessing

Run model prediction

Return:

churn: Yes/No

probability score

🛠️ Troubleshooting
Problem	Fix
Flask won't start	Check port or reinstall Flask
Model not found	Run customer_churn_prediction.py first
Wrong input format	Ensure field names match training features
Unseen category error	Set handle_unknown="ignore" in encoder
Type conversion errors	Ensure numeric fields are parsed properly
🚀 Possible Improvements

Create scikit-learn Pipeline to simplify preprocessing

Add Docker support

Add SHAP explainability graphs

Deploy on Render / Railway / AWS

Add responsive frontend styling

📜 Dataset & License

The Telco Customer Churn dataset is publicly available (often from Kaggle).
Check original licensing before redistribution.

🤝 Need Help?

If you want, I can also generate:

A cleaner UI for index.html

A full pipeline version of customer_churn_prediction.py

A production-ready app.py

A Dockerfile for deployment

Just say the word, George 🔥
