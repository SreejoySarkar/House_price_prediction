# 🏠 House Price Prediction

A full-stack machine learning web application that predicts house prices based on area (sq ft) and number of rooms.

- **Backend**: Flask REST API  
- **Frontend**: Streamlit  
- **ML Model**: Linear Regression (scikit-learn)  
- **Dataset**: `data/house_price.csv` (47 samples — area, rooms, price)

---

## Project Structure

```
house_price_project/
├── data/
│   └── house_price.csv       # Dataset
├── model/
│   ├── model.pkl             # Trained model (generated)
│   ├── scaler.pkl            # StandardScaler (generated)
│   └── diagnostics.png       # Eval plots (generated)
├── backend/
│   └── app.py                # Flask REST API
├── frontend/
│   └── ui.py                 # Streamlit UI
├── train_model.py            # Model training script
├── requirements.txt
└── README.md
```

---

## Quickstart

### 1. Install dependencies
```bash
pip install -r requirements.txt
```

### 2. Train the model
```bash
python train_model.py
```
This saves `model/model.pkl` and `model/scaler.pkl`.

### 3. Start the Flask backend
```bash
python backend/app.py
```
API runs at **http://localhost:5000**

### 4. Launch the Streamlit frontend  
*(open a second terminal)*
```bash
streamlit run frontend/ui.py
```
UI opens at **http://localhost:8501**

---

## API Endpoints

| Method | Endpoint       | Description                          |
|--------|----------------|--------------------------------------|
| GET    | `/health`      | Health check                         |
| POST   | `/predict`     | Predict house price                  |
| GET    | `/dataset`     | Return full dataset as JSON          |
| GET    | `/model_info`  | Model coefficients + metrics         |

### POST `/predict` — example
```json
// Request
{ "area": 2000, "rooms": 3 }

// Response
{
  "area": 2000.0,
  "rooms": 3.0,
  "predicted_price": 347820.50,
  "currency": "USD"
}
```

---

## Frontend Pages

| Page                | Description                                        |
|---------------------|----------------------------------------------------|
| **Predict Price**   | Input area + rooms, get instant price + gauge chart |
| **Dataset Explorer**| Browse data, scatter/histogram/box/heatmap charts  |
| **Model Insights**  | R², MAE, RMSE, coefficients, regression trendline  |

---

## Model Performance (typical)

| Metric | Value         |
|--------|---------------|
| R²     | ~0.73         |
| MAE    | ~$40,000      |
| RMSE   | ~$55,000      |

---

## Tech Stack

| Layer     | Technology              |
|-----------|-------------------------|
| ML        | scikit-learn, numpy     |
| Backend   | Flask                   |
| Frontend  | Streamlit, Plotly       |
| Data      | pandas, matplotlib      |
