# 🏠 House Price Prediction

<p align="center">
  <strong>A Machine Learning project for predicting house prices using area and number of rooms.</strong><br/>
  Built with Python, Scikit-learn, Pandas, NumPy and Flask-ready ML components.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.x-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python">
  <img src="https://img.shields.io/badge/Scikit--learn-1.5.1-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white" alt="Scikit-learn">
  <img src="https://img.shields.io/badge/Pandas-2.2.2-150458?style=for-the-badge&logo=pandas&logoColor=white" alt="Pandas">
  <img src="https://img.shields.io/badge/NumPy-1.26.4-013243?style=for-the-badge&logo=numpy&logoColor=white" alt="NumPy">
  <img src="https://img.shields.io/badge/Flask-3.0.3-000000?style=for-the-badge&logo=flask&logoColor=white" alt="Flask">
</p>

---

## 📌 Overview

**House Price Prediction** is a supervised machine learning project that estimates the price of a house from two primary features:

- 📐 **Area** — house size in square feet
- 🛏️ **Rooms** — number of rooms

The project demonstrates a complete basic machine-learning workflow:

**Dataset → Data Preparation → Train/Test Split → Feature Scaling → Linear Regression → Evaluation → Model Serialization → Prediction**

The model is implemented using **Linear Regression** from Scikit-learn, with **StandardScaler** used to normalize the input features before training.

> **Note:** This repository currently contains the training script, dependency configuration and project report. The training script expects the dataset at `data/house_price.csv`. If the dataset is not present in your local checkout, add it before running the training script.

---

## ✨ Key Features

| Feature | Description |
|---|---|
| 📊 Data Loading | Loads house-price data using Pandas |
| 🔍 Feature Selection | Uses `area` and `rooms) as model inputs |
| ✂️ Train/Test Split | Uses an 80/20 split for evaluation |
| ⚖️ Feature Scaling | Applies `StandardScaler` to numerical features |
| 🤖 ML Algorithm | Linear Regression |
| 📈 Evaluation | Calculates MAE, RMSE and R² |
| 💾 Model Persistence | Saves trained model and scaler using Joblib |
| 📉 Diagnostics | Generates actual-vs-predicted and residual plots |
| 🌐 API-Ready | Dependencies include Flask and Requests for application integration |

---

## 🧠 Machine Learning Workflow

### 1. Load the dataset

The project reads the CSV dataset with Pandas:

```text
data/house_price.csv
```

The expected columns are:

| Column | Type | Description |
|---|---|---|
| `area` | Numeric | House area in square feet |
| `rooms` | Numeric | Number of rooms |
| `price` | Numeric | Target house price |

---

### 2. Select features and target

The model uses:

```python
X = df[["area", "rooms"]]
y = df["price"]
```

Where:

- **X** = independent/input variables
- **y** = dependent/target variable

---

### 3. Split the data

The dataset is divided into training and testing sets:

- **80%** → Training
- **20%** → Testing
- `random_state=42` → makes the split reproducible

This allows the model to be evaluated on data that was not used during training.

---

### 4. Standardize the features

The project uses Scikit-learn's `StandardScaler`:

```python
scaler = StandardScaler()
X_train_sc = scaler.fit_transform(X_train)
X_test_sc = scaler.transform(X_test)
```

The scaler is fitted only on the training data and then applied to the test data. This avoids leaking information from the test set into the training process.

---

### 5. Train the Linear Regression model

The model is created with:

```python
model = LinearRegression()
model.fit(X_train_sc, y_train)
```

Conceptually, the model learns a relationship of the form:

```text
Predicted Price = Intercept
                + (Coefficient₁ × Area)
                + (Coefficient₂ × Rooms)
```

Because the features are standardized before training, the learned coefficients represent the relationship using the scaled feature values.

---

## 📊 Model Evaluation

The project evaluates predictions using three standard regression metrics.

### Mean Absolute Error — MAE

MAE measures the average absolute difference between actual and predicted prices.

```text
MAE = average(|actual - predicted|)
```

**Lower MAE is better.**

---

### Root Mean Squared Error — RMSE

RMSE gives greater weight to larger prediction errors.

```text
RMSE = sqrt(mean((actual - predicted)²))
```

**Lower RMSE is better.**

---

### R² Score

R² measures how much of the variation in the target variable is explained by the model.

```text
R² = 1 - (Residual Sum of Squares / Total Sum of Squares)
```

A value closer to **1.0** indicates that the model explains more of the observed variation in the target data.

> Evaluation results depend on the exact dataset and train/test split. The repository should be run locally to obtain the current MAE, RMSE and R² values rather than treating example values as fixed results.

---

## 📉 Model Diagnostics

After training, the script generates:

### Actual vs Predicted

A scatter plot comparing the real house prices with the model's predictions.

Points closer to the diagonal reference line indicate smaller prediction errors.

### Residual Distribution

A histogram of:

```text
Residual = Actual Price - Predicted Price
```

Residual analysis helps identify whether the model's errors are centered around zero and whether unusually large errors are present.

The generated diagnostic image is saved as:

```text
model/diagnostics.png
```

---

## 💾 Saved Model Files

After successful training, Joblib saves:

```text
model/
├── model.pkl
└── scaler.pkl
```

### `model.pkl`

Contains the trained Scikit-learn Linear Regression model.

### `scaler.pkl`

Contains the fitted StandardScaler required to transform new input features in the same way as the training data.

Keeping both files is important: a prediction pipeline must use the same preprocessing transformation that was applied during training.

---

## 📁 Project Structure

The current repository is organized around the following files:

```text
House_price_prediction/
│
├── README.md
│   └── Project documentation
│
├── SreejoySarkar_HousePricePrediction.py
│   └── Data loading, preprocessing, training,
│       evaluation, model saving and diagnostics
│
├── requirements.txt
│   └── Python dependencies
│
└── SreejoySarkar_ProjectReport.docx
    └── Detailed project report
```

### Runtime-generated / expected files

The training script expects:

```text
data/
└── house_price.csv
```

and creates:

```text
model/
├── model.pkl
├── scaler.pkl
└── diagnostics.png
```

---

## 🛠️ Tech Stack

### Programming Language

- **Python**

### Machine Learning

- **Scikit-learn**
- **Linear Regression**
- **StandardScaler**

### Data Processing

- **Pandas**
- **NumPy**

### Model Persistence

- **Joblib**

### Visualization

- **Matplotlib**
- **Seaborn**
- **Plotly**

### Application/API Support

- **Flask**
- **Requests**

---

## 📦 Dependencies

The project pins the main dependencies to specific versions for reproducibility:

```text
Flask==3.0.3
scikit-learn==1.5.1
pandas==2.2.2
numpy==1.26.4
joblib==1.4.2
streamlit==1.36.0
requests==2.32.3
matplotlib==3.9.1
seaborn==0.13.2
plotly==5.22.0
```

---

## 🚀 Getting Started

### Prerequisites

Make sure you have:

- Python 3.x
- pip
- Git

Check your installation:

```bash
python --version
pip --version
```

---

### 1. Clone the repository

```bash
git clone https://github.com/SreejoySarkar/House_price_prediction.git
cd House_price_prediction
```

---

### 2. Create a virtual environment

#### Windows

```bash
python -m venv venv
venv\\Scripts\\activate
```

#### macOS / Linux

```bash
python3 -m venv venv
source venv/bin/activate
```

---

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

---

### 4. Add the dataset

Create the required directory:

```text
data/
```

Place the dataset here:

```text
data/house_price.csv
```

The CSV should contain at least:

```text
area,rooms,price
```

---

### 5. Train the model

Run:

```bash
python SreejoySarkar_HousePricePrediction.py
```

The script will:

1. Load the dataset
2. Display dataset information
3. Split the data
4. Scale the features
5. Train Linear Regression
6. Generate predictions
7. Calculate MAE, RMSE and R²
8. Save the model
9. Save the scaler
10. Generate diagnostic plots

---

## 🧪 Example Training Output

Your exact values will depend on the dataset:

```text
Dataset shape: (...)

-- Model Evaluation --
  MAE  : $...
  RMSE : $...
  R2   : ...

Model and scaler saved to /model.
Diagnostics plot saved: .../model/diagnostics.png
```

---

## 🔮 Making a Prediction

Once the model and scaler have been generated, a new house can be represented by:

```python
new_house = [[2000, 3]]
```

The input must first be transformed using the saved scaler:

```python
import joblib

model = joblib.load("model/model.pkl")
scaler = joblib.load("model/scaler.pkl")

new_house_scaled = scaler.transform([[2000, 3]])
prediction = model.predict(new_house_scaled)

print(prediction)
```

This produces the model's estimated house price.

---

## ⚠️ Important Limitations

This project is designed as an educational machine-learning application and should not be treated as a production-grade property valuation system.

### Limited feature set

The model uses only:

- Area
- Number of rooms

Real-world house prices can also depend on:

- Location
- Neighborhood
- Property age
- Floor number
- Number of bathrooms
- Parking
- Property condition
- Amenities
- Nearby schools and transportation
- Local market conditions

### Dataset size

A small dataset can limit generalization. More representative data would be required for reliable real-world predictions.

### Linear relationship assumption

Linear Regression assumes a linear relationship between the input features and target. Real estate markets can contain nonlinear relationships and interactions that this model may not capture.

### Geographic variation

A model trained on one housing market may perform poorly when applied to another market.

---

## 🔐 Reproducibility

The project uses:

```python
random_state=42
```

for the train/test split, making the split deterministic when the same dataset and environment are used.

Dependencies are also version-pinned in `requirements.txt` to improve reproducibility.

---

## 🔄 End-to-End Pipeline

```text
                  ┌─────────────────────┐
                  │   House Price CSV   │
                  └──────────┬──────────┘
                             │
                             ▼
                  ┌─────────────────────┐
                  │   Load with Pandas  │
                  └──────────┬──────────┘
                             │
                             ▼
                  ┌─────────────────────┐
                  │ Select area + rooms │
                  └──────────┬──────────┘
                             │
                             ▼
                  ┌─────────────────────┐
                  │   Train/Test Split  │
                  └──────────┬──────────┘
                             │
                             ▼
                  ┌─────────────────────┐
                  │   StandardScaler    │
                  └──────────┬──────────┘
                             │
                             ▼
                  ┌─────────────────────┐
                  │  Linear Regression  │
                  └──────────┬──────────┘
                             │
                ┌────────────┴────────────┐
                ▼                         ▼
      ┌──────────────────┐      ┌──────────────────┐
      │ Model Evaluation │      │ Model Persistence│
      │ MAE / RMSE / R²  │      │ model + scaler   │
      └────────┬─────────┘      └──────────────────┘
               │
               ▼
      ┌──────────────────┐
      │ Diagnostic Plots │
      └──────────────────┘
```

---

## 🎯 Learning Objectives

This project demonstrates practical understanding of:

- Supervised machine learning
- Regression problems
- Feature selection
- Train/test splitting
- Feature standardization
- Linear Regression
- Model evaluation
- Error analysis
- Model serialization
- Python data science workflows
- Reproducible machine-learning experiments

---

## 🚧 Future Improvements

Possible extensions include:

- [ ] Add a larger real-world housing dataset
- [ ] Add location/geographic features
- [ ] Add bathrooms, parking and property-age features
- [ ] Compare Linear Regression with Random Forest, Gradient Boosting and XGBoost
- [ ] Add cross-validation
- [ ] Add hyperparameter tuning
- [ ] Add feature-importance analysis
- [ ] Add a complete Flask prediction API
- [ ] Add a Streamlit interactive frontend
- [ ] Add automated tests
- [ ] Add Docker support
- [ ] Add CI/CD with GitHub Actions
- [ ] Deploy the prediction service online

---

## 📄 Project Report

A detailed project report is included in:

```text
SreejoySarkar_ProjectReport.docx
```

It can be used alongside the source code to understand the project's methodology and implementation.

---

## 👨‍💻 Author

**Sreejoy Sarkar**

GitHub: [@SreejoySarkar](https://github.com/SreejoySarkar)

---

## 📜 License

No explicit license is currently declared in this repository.

If you intend to allow others to reuse, modify or distribute the project, consider adding an appropriate open-source license such as MIT.

---

## ⭐ Support

If this project is useful for learning or reference, consider giving the repository a ⭐ on GitHub.

---

<p align="center">
  <strong>Built with Python & Machine Learning 🤖</strong>
</p>
