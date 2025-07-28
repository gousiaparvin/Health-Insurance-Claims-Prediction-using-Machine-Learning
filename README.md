# Health-Insurance-Claims-Prediction-using-Machine-Learning
# Project Title
Health Insurance Claim Prediction Using Machine Learning

# 🎯 Aim of the Project
To develop a machine learning model that accurately predicts the insurance claim amount based on various health, lifestyle, and demographic factors of individuals. The goal is to assist insurance companies in forecasting claim costs and risk assessment.

# 📊 Dataset Used
File name: health_insurance.csv

Size: 15,000 records × 13 columns

# Features include:

Age, Sex, BMI, Weight

Health factors: Blood Pressure, Diabetes, Hereditary Diseases, Smoker, Exercise

Location: City

Employment: Job Title

Target Variable: claim (insurance claim amount)

# 🔁 Process Workflow Summary
# 🔹 1. Data Loading & Cleaning
Loaded dataset using pandas

Handled missing values in bmi (filled with mean) and age (mode)

Removed duplicates

# 🔹 2. Exploratory Data Analysis (EDA)
Used Seaborn and Matplotlib for:

Pie charts: gender, smoker status, diabetes, exercise habits

Correlation heatmaps

BMI analysis across job titles

Age & smoker-wise insurance claim trends

Boxplot & bar plots for claim insights by sex, health status

# 🔹 3. Feature Engineering
Label Encoding for categorical columns: sex, city, job_title, hereditary_diseases

Standardization using StandardScaler to normalize features

# 🧠 Machine Learning Models Applied
Model	R² Score	RMSE
Linear Regression	0.744	0.499
ARD Regression	0.744	0.499
Huber Regressor	0.715	0.527
Lasso Regression	~0.00	0.987
Tweedie Regressor	0.593	0.629
Support Vector Regressor	0.866	0.362
KNeighbors Regressor	0.947	0.228
Decision Tree Regressor	0.954	0.212
XGBoost Regressor	0.963	0.189
Random Forest Regressor	0.972	0.165

✅ Best Performing Model: Random Forest Regressor

# Model Deployment: Real-Time Insurance Claim Prediction Web App
To make the insurance claim prediction model accessible to users, I deployed the trained Random Forest Regressor using a Flask-based web application.

🧩 Deployment Components
✅ 1. Model Serialization
The best-performing model (RandomForestRegressor, R² ≈ 97.2%) was saved using joblib:

python
Copy
Edit
joblib.dump(rfc, 'model.pkl', compress=4)

✅ 2. Flask App Development
Created a Python Flask server to handle:

Homepage (/): Displays a form to input user health/demographic data.

Prediction route (/predict): Handles form submission, processes data, performs prediction, and returns results.


✅ 3. Input Processing Logic
Categorical inputs (e.g., sex, smoker, city, job title, hereditary disease) were mapped to encoded integers using dictionaries:

python
Copy
Edit
sex = 1 if sex_select == 'MALE' else 0
city = cities[city_select]
job_title = job_titles[job_title_selected]
...

✅ 4. Prediction and Post-Processing
Inputs passed to the model as a 2D array:

python
Copy
Edit
predictions = model.predict([[...]])
The output (which was normalized) was scaled back to the original currency unit:

python
Copy
Edit
output = predictions[0] * 12147.834670761482
Result was formatted and displayed to the user:

python
Copy
Edit
"Your estimated health insurance claim is $xx,xxx.xx"

✅ 5. Web Hosting
The app was hosted locally:

python
Copy
Edit
app.run(port=8080)
Accessible via browser at: http://127.0.0.1:8080/

# 🌐 Deployment Outcome
Interactive, real-time prediction system for health insurance claims.

Allows input of 13 health and demographic parameters.

Returns predictions in a user-friendly, formatted output.

Demonstrates full ML lifecycle integration: Data cleaning → Modeling → Evaluation → Deployment.

# 💾 Model Deployment Step
Model saved as model.pkl using joblib.dump()

Reloaded and tested with joblib.load()

Ready for deployment into a web service or Flask/Streamlit app

# ⚙️ Key Functions & Why They Were Used
Function/Method	Purpose
LabelEncoder()	Convert categorical variables into numeric
StandardScaler()	Normalize feature values for better model performance
train_test_split()	Split dataset into training and test sets
LinearRegression(), SVR() etc.	Train multiple regression models
mean_squared_error()	Calculate RMSE for error evaluation
R² Score	Measures how well predicted values match actual claims
joblib.dump/load()	Save and reload trained model for deployment

# 📈 Insights Derived
Smokers and diabetics tend to have higher insurance claims.

Government employees and photographers have higher BMI on average.

Exercise, age, and hereditary disease status also influence claims.

Male individuals and non-exercising individuals had higher average claim amounts.


# 📌 Tools & Technologies
Python, Flask, HTML (Jinja templates) for UI

Scikit-learn, XGBoost, Joblib for modeling and persistence

Matplotlib, Seaborn, Pandas for data analysis and EDA

# 🚀 Future Scope
Build a web-based interface using Flask or Streamlit to input new patient data and return predictions.

Integrate SHAP or LIME for explainable AI and feature contribution analysis.

Introduce real-time data ingestion (e.g., from wearable devices).

Include cost-benefit analysis for insurance pricing strategies.

Improve performance using ensemble stacking or neural networks.

