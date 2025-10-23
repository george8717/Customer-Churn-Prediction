to activate virtual env
python -m venv venv
venv\Scripts\activate



Let’s go step by step — I’ll show you how to:

Check library versions in Colab

Match those versions in VS Code

Create & activate a virtual environment

Install the exact dependencies

Run the backend + frontend properly

🧩 STEP 1: Check Python & library versions in Google Colab

Run the following in your Colab notebook:

import sys
import sklearn
import numpy
import pandas
import joblib

print("Python:", sys.version)
print("scikit-learn:", sklearn.__version__)
print("numpy:", numpy.__version__)
print("pandas:", pandas.__version__)
print("joblib:", joblib.__version__)


Example output (typical for Colab as of Oct 2025):

Python: 3.10.12
scikit-learn: 1.5.1
numpy: 1.26.4
pandas: 2.2.2
joblib: 1.4.2


Keep those numbers handy.

⚙️ STEP 2: Create project folder locally

Open VS Code, and create a folder, e.g.:

folder name/
│
├── app.py
├── placement_model.pkl
├── index.html
└── requirements.txt

🧱 STEP 3: Create and activate a virtual environment
On Windows (PowerShell or CMD)
python -m venv venv
venv\Scripts\activate

On macOS/Linux
python3 -m venv venv
source venv/bin/activate


Once activated, your terminal will show (venv) in front.

📦 STEP 4: Create requirements.txt

Make a file requirements.txt in your folder and copy your Colab versions:

Flask==3.0.3
numpy==1.26.4
pandas==2.2.2
scikit-learn==1.5.1
joblib==1.4.2


Now install all dependencies:

pip install -r requirements.txt


✅ This ensures your VS Code environment matches your Colab exactly.

💻 STEP 5: Flask backend (app.py)

Here’s the version that will work smoothly with those library versions:

from flask import Flask, request, jsonify, render_template
import joblib
import numpy as np

app = Flask(__name__, template_folder='.')

# Load your trained model
model = joblib.load('placement_model.pkl')

@app.route('/')
def home():
    return render_template('index.html')

@app.route('/predict', methods=['POST'])
def predict():
    data = request.get_json(force=True)
    features = np.array(data['features']).reshape(1, -1)
    prediction = model.predict(features)
    return jsonify({'prediction': int(prediction[0])})

if __name__ == '__main__':
    app.run(debug=True)

🎨 STEP 6: Frontend (index.html)
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Placement Prediction</title>
    <style>
        body { font-family: Arial; text-align: center; margin-top: 60px; }
        input, button { margin: 8px; padding: 10px; font-size: 16px; }
        #result { margin-top: 20px; font-weight: bold; }
    </style>
</head>
<body>
    <h2>🎓 Placement Prediction App</h2>
    <input type="number" id="feature1" placeholder="Enter feature 1 (e.g., 7.0)">
    <input type="number" id="feature2" placeholder="Enter feature 2 (e.g., 100.0)">
    <br>
    <button onclick="predict()">Predict</button>
    <p id="result"></p>

    <script>
        async function predict() {
            const f1 = parseFloat(document.getElementById('feature1').value);
            const f2 = parseFloat(document.getElementById('feature2').value);
            const response = await fetch('/predict', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ features: [f1, f2] })
            });
            const result = await response.json();
            document.getElementById('result').innerText =
                result.prediction === 1 ? "✅ Placed" : "❌ Not Placed";
        }
    </script>
</body>
</html>

▶️ STEP 7: Run it

Make sure you’ve activated your virtual environment, then run:

python app.py


Visit http://127.0.0.1:5000

and you’ll see your frontend connected to your backend 💫

🧩 Optional: Generate requirements.txt Automatically

If you want to export exact versions from your environment:

pip freeze > requirements.txt


This ensures your app can be deployed anywhere with identical dependencies.
