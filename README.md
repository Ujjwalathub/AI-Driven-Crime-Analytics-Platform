🛡️ KSP AI-Driven Crime Analytics Platform

A comprehensive, AI-powered analytics and visualization platform built for the Karnataka State Police (KSP) Datathon 2026 (Challenge 2).

This platform transforms fragmented, siloed crime records into actionable intelligence. By leveraging machine learning, geospatial clustering, and graph theory, it enables law enforcement to proactively track repeat offenders, detect crime hotspots, and uncover hidden criminal networks.

✨ Key Features

📈 Predictive Anomaly Engine: Utilizes an Isolation Forest ML model to detect multi-dimensional anomalies and statistically significant crime spikes (e.g., sudden surges in vehicle thefts).

🗺️ Geospatial Hotspot Mapping: Interactive scatter mapping and KDE density heatmaps to visualize high-risk zones across major Karnataka districts (Bengaluru, Mysuru, Hubballi, etc.).

🕸️ Network Link Analysis: Applies Graph Theory (Degree & Betweenness Centrality via NetworkX) to map criminal syndicates, automatically identifying priority targets ("Kingpins") and key network brokers.

📊 Real-Time Interactive Dashboard: A highly responsive React frontend featuring actionable metrics, demographic breakdowns, and time-series forecasting.

🏗️ System Architecture

The application follows a modern, decoupled 3-Tier Architecture:

Data & ML Layer (Backend Memory/Scikit-Learn): Ingests enriched synthetic CSV data and runs Machine Learning models.

API Layer (FastAPI): Acts as the bridge, executing ML predictions and serving the results as structured JSON.

Presentation Layer (React): Consumes the API endpoints asynchronously and renders the interactive dashboard.

Data Flow

[ Enriched CSV Data ] 
        │ (Loaded on startup)
        ▼
[ FastAPI Server (main.py) ] ◄───► [ Scikit-Learn ML Engine ]
        │                             (Isolation Forest, etc.)
        │ (RESTful JSON API)
        ▼
[ React Frontend (App.jsx) ]
  ├─ Timeline Chart (Reads Anomaly Data)
  ├─ Geospatial Map (Reads Hotspot Data)
  └─ Network Graph (Reads Kingpin/Centrality Data)


🛠️ Technology Stack

Frontend: React, Tailwind CSS, Recharts, Lucide-React

Backend: Python, FastAPI, Uvicorn

Data Science & ML: Scikit-Learn (Isolation Forest, Random Forest), Pandas, NumPy, SciPy

Graph Analytics: NetworkX, Python-Louvain

Data Generation: Faker (Synthetic Indian demographic data)

🚀 Execution Protocol (Local Setup)

To test the end-to-end integration smoothly, you must start the backend API before the frontend application.

1. Start the ML Backend

Open a terminal and navigate to the backend directory containing main.py and the .csv datasets (criminals_enriched.csv, incidents_time_engineered.csv, etc.).

# Install required Python dependencies
pip install scikit-learn pandas numpy fastapi uvicorn networkx

# Run the FastAPI server
uvicorn main:app --reload --port 8000


Verify: Open http://127.0.0.1:8000/docs in your browser to view the Swagger API documentation and confirm the ML models are initialized.

2. Start the React Frontend

Open a second terminal and navigate to your React project directory.

# Install Node.js dependencies
npm install recharts lucide-react

# Start the development server
npm start
# (or `npm run dev` if using Vite)


Verify: Open http://localhost:3000. The application will automatically hit the FastAPI endpoints and populate the dashboard with ML-driven insights.

🔌 API Contracts

The FastAPI backend exposes the following endpoints for the frontend to consume:

Endpoint

Method

Payload Returned (JSON)

ML Model Integrated

/api/v1/overview/stats

GET

{"total_incidents": 50000, ...}

None (Aggregation)

/api/v1/analytics/timeline

GET

[{"date": "2025-10-01", "incidents": 340, "isAnomaly": true}]

Isolation Forest

/api/v1/geospatial/hotspots

GET

[{"x": 77.59, "y": 12.97, "type": "Theft"}]

DBSCAN (Pending)

/api/v1/network/kingpins

GET

[{"id": "uuid", "name": "...", "threat_level": "High"}]

Graph Theory (Centrality)

🧪 About the Data (Synthetic Datasets)

Due to the highly confidential nature of the State Crime Records Bureau (SCRB) databases, this prototype utilizes highly realistic synthetic data.

A custom Python pipeline (generate_ksp_data.py) was built to generate 50,000+ incidents and 5,000+ criminal profiles. The data strictly adheres to real-world statistical distributions:

Spatial: Geographically bounded to Karnataka using Gaussian clusters around 5 major cities.

Relational: Networks generated using the Barabási–Albert Preferential Attachment Model to simulate real scale-free criminal syndicates.

Temporal: Programmatic injection of statistical anomalies to validate the ML Isolation Forest model.

Detailed Exploratory Data Analysis (EDA) validating this data can be found in the accompanying Jupyter Notebooks.
