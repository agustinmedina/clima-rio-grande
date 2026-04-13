# 🌧️ Climate Prediction — Rio Grande do Sul, Brazil

A data science project built to predict rainfall and analyze the impact of extreme weather events on crops in Rio Grande do Sul — the Brazilian state hit by its worst flooding in history in 2024.

> **Learning project** — replicated and extended from a team project as part of my data science learning journey.

---

## 🌐 Live Demo

👉 [prediccionlluviaenriograndedosul.streamlit.app](https://prediccionlluviaenriograndedosul.streamlit.app/)

---

## 📌 What it does

- Fetches **real-time hourly weather forecasts** from OpenWeather API
- Displays temperature, humidity, wind speed and precipitation for any selected date
- Shows a **weather condition icon** based on current forecast (rain, storm, sunny, cloudy)
- Includes a **trained ML classification model** to predict rain likelihood
- Connects to **10 years of historical climate data** (2014–2024) for analysis

---

## 🏗️ Architecture

```
OpenWeather API
      │
      ▼
Apache Airflow DAG          ← runs daily at midnight
(climadag.py)
      │
      ▼
Google Cloud Storage        ← stores daily CSV
      │
      ▼
BigQuery                    ← historical data warehouse
      │
      ├──▶ Power BI Dashboard   ← crop impact visualization
      │
      └──▶ Streamlit App        ← live weather prediction
              +
           ML Model (.pkl)
```

---

## 🛠️ Tech Stack

| Layer | Tools |
|---|---|
| Data ingestion | Python, OpenWeather API, Apache Airflow |
| Cloud storage | Google Cloud Storage, BigQuery |
| Machine learning | Scikit-learn, Pandas, NumPy |
| Web app | Streamlit |
| Dashboard | Power BI |
| Automation | Airflow DAGs, Docker |

---

## 📊 Dataset

- **Source:** OpenWeather API (One Call 3.0 — historical day summary)
- **Location:** Porto Alegre, Rio Grande do Sul (-30.03, -51.21)
- **Period:** January 2014 – June 2024
- **Records:** 3,811 daily observations
- **Features:** min/max temperature, afternoon temperature, morning temperature, evening temperature, night temperature, humidity, total precipitation, pressure, max wind speed, wind direction, cloud cover

---

## 🤖 ML Model

The classification model (`modelo_clasificacion.pkl`) was trained using Scikit-learn to predict rain conditions based on meteorological variables.

Training notebook: [`entrenar_ml.ipynb`](notebooks/entrenar_ml.ipynb)  
EDA notebook: [`eda.ipynb`](notebooks/eda.ipynb)

---

## 🚀 Run locally

**1. Clone the repo**
```bash
git clone https://github.com/YOUR_USERNAME/clima-portfolio.git
cd clima-portfolio
```

**2. Create and activate virtual environment**
```bash
python -m venv venv

# Windows
venv\Scripts\activate

# Mac/Linux
source venv/bin/activate
```

**3. Install dependencies**
```bash
pip install streamlit pandas requests python-dotenv scikit-learn joblib
```

**4. Set up your API key**

Create a `.env` file in the root folder:
```
api=YOUR_OPENWEATHER_API_KEY
```
Get a free key at [openweathermap.org](https://openweathermap.org/api)

**5. Run the app**
```bash
streamlit run modelo_lluvia.py
```

Open [http://localhost:8501](http://localhost:8501) in your browser.

---

## 📁 Project structure

```
clima-portfolio/
├── modelo_lluvia.py          # Streamlit app
├── modelo_clasificacion.pkl  # trained ML model
├── datos_clima.csv           # historical dataset (2014–2024)
├── .env                      # API key (not committed)
├── .gitignore
├── requirements.txt
├── img/                      # weather condition icons
│   ├── lluvia.png
│   ├── lluvia_moderada.png
│   ├── nubes_dispersas.png
│   ├── nublado.png
│   ├── soleado.png
│   └── tormenta.png
├── notebooks/
│   ├── eda.ipynb
│   └── entrenar_ml.ipynb
└── dags/                     # Airflow pipeline (GCP setup)
    ├── climadag.py
    ├── bqdag.py
    └── src/
        └── extraccion_clima.py
```

---

## 🌎 Context

Rio Grande do Sul has a documented history of flooding — the most recent major events were in 2015, 2020, and 2024. The **2024 floods were the most severe in the state's recorded history**, affecting hundreds of thousands of people and causing massive damage to agriculture.

This project aims to provide a tool that anticipates extreme weather conditions and estimates the economic impact on key regional crops (soy, rice, corn, wheat, canola, and more).

---

## 📄 License

MIT — free to use and adapt with attribution.
