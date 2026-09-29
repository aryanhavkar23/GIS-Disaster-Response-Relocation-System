# 🛰️ Intelligent GIS-Based Proactive Relocation Decision Support System (GeoDSS)

[![SIH 2026](https://img.shields.io/badge/SIH-2026-orange.svg?style=for-the-badge)](https://www.sih.gov.in/)
[![Problem Statement](https://img.shields.io/badge/PS_ID-191-blue.svg?style=for-the-badge)](https://www.sih.gov.in/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.110+-009688.svg?style=for-the-badge&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![React 18](https://img.shields.io/badge/React-18.3-61DAFB.svg?style=for-the-badge&logo=react&logoColor=black)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Vite-5.4-646CFF.svg?style=for-the-badge&logo=vite&logoColor=white)](https://vitejs.dev/)
[![PostGIS](https://img.shields.io/badge/PostGIS-Spatial_DB-336791.svg?style=for-the-badge&logo=postgresql&logoColor=white)](https://postgis.net/)
[![Leaflet](https://img.shields.io/badge/WebGIS-Leaflet-199900.svg?style=for-the-badge&logo=leaflet&logoColor=white)](https://leafletjs.com/)

> **"Don't wait for a disaster to happen. Identify high-risk habitations in advance, determine safer relocation locations, and help authorities prioritize relocation decisions using GIS, multi-hazard analysis, AI, and data-driven decision support."**

---

## 📌 Executive Summary

Disaster management in hazard-prone regions (Western Ghats, Himalayan arc, coastal zones) has historically operated in a **reactive cycle**: disaster strikes, emergency rescue is deployed, makeshift relief camps are established, and communities inevitably rebuild in the very same hazard paths.

The **Intelligent GIS-Based Proactive Relocation Decision Support System (PS ID 191)** shifts this paradigm from **reactive rescue** to **proactive, data-driven prevention**. By combining high-resolution satellite Earth observation data, multi-hazard spatial analytics, machine learning, and carrying capacity models, the platform answers four critical governance questions:

| # | Administrative Question | System Resolution Mechanism |
|---|---|---|
| **Q1** | **Which areas are strictly unsafe for human settlement?** | Multi-hazard spatial overlay of slope stability, landslide susceptibility, and flood inundation to demarcate dynamic **Red Zones**. |
| **Q2** | **Which specific habitations face imminent danger?** | Spatial intersection of revenue villages with Red Zones, computing composite **Habitation Vulnerability Indices (HVI)**. |
| **Q3** | **Where can affected populations safely relocate?** | Multi-criteria spatial suitability engine evaluating low-hazard terrain, gentle slopes, road access, and environmental safety. |
| **Q4** | **Can the candidate sites sustainably absorb the population?** | **Carrying Capacity Auditing Engine** calculating per-capita land ($45\,\text{m}^2/\text{person}$), potable water, healthcare, and education thresholds. |
| **Q5** | **Who must be relocated first, and on what timeline?** | Algorithmic **Relocation Prioritization Matrix** triaging habitations into *Immediate (P1)*, *Short-Term (P2)*, *Medium-Term (P3)*, and *In-Situ Monitoring*. |

---

## 🚀 Key Features

### 1. 🗺️ Interactive WebGIS Command Center
- Full-screen interactive map powered by Leaflet & OpenStreetMap tiles.
- Layer toggles for **Copernicus DEM slope gradients**, **Multi-Hazard Red Zones**, **Vulnerable Habitations**, and **Candidate Relocation Parcels**.
- Visual indicators for isolation risk, road lifelines, and distance buffers.

### 2. ⚠️ Multi-Hazard Risk & Dynamic Red Zone Demarcation
- Integrates terrain slope, topographic wetness index (TWI), and precipitation anomalies.
- Automatic spatial clustering and dynamic hazard buffering around active geomorphic fault lines and floodplains.

### 3. 🔍 Habitation Vulnerability Profiling & Explainable AI (XAI)
- Granular breakdown of composite risk: $\text{Risk} = \text{Hazard} \times \text{Exposure} \times \text{Vulnerability}$.
- **Transparent Attribution**: Explains *why* a village is flagged (e.g., Slope $> 32^\circ$, 3-day rainfall anomaly, cut-off access roads, high kutcha housing ratio).

### 4. 📍 Candidate Site Suitability Engine
- Automated constraint filtering (excludes slopes $> 15^\circ$, ecological reserves, floodplains, and hazard buffers).
- Multi-factor AHP suitability scoring across road connectivity, groundwater table, health clinics, and schools.

### 5. ⚖️ Recipient Carrying Capacity Auditing
- Enforces statutory planning norms (e.g., $45\,\text{m}^2$ land per capita, $135\,\text{LPD}$ water requirement).
- Real-time Capacity Factor calculation ($\text{Available Capacity} / \text{Target Population}$) to prevent secondary disasters or slum creation.

### 6. 📊 Phased Relocation Prioritization Queue
- Algorithmic triage ranking settlements by urgency:
  - 🔴 **Priority 1 (Immediate)**: Habitations with critical risk ($\ge 75$) and direct Red Zone intersection.
  - 🟠 **Priority 2 (Short-Term)**: High-risk habitations requiring planned seasonal relocation.
  - 🟡 **Priority 3 (Medium-Term)**: Moderate-risk habitations slated for phased resettlement.
  - 🟢 **In-Situ Mitigation**: Settlements where structural engineering defenses suffice.

### 7. 🧪 "What-If" Policy Simulation Sandbox
- Interactive parametric testing for State Relief Commissioners and District Collectors.
- Dynamically simulate scenarios such as:
  - *Increased monsoon intensity (+25% rainfall anomaly)*
  - *Stricter Red Zone thresholds ($75 \to 60$)*
  - *Infrastructure upgrades (new arterial access roads or flood barriers)*

### 8. 📄 Statutory Relocation Action Dossiers
- One-click generation of official administrative briefing dossiers per habitation, formatted for SDMA/DDMA decision-makers under Section 38 of the Disaster Management Act.

---

## 🏗️ System Architecture

```text
┌──────────────────────────────────────────────────────────────────────────────────┐
│                             PRESENTATION LAYER (WebGIS)                          │
│     React 18 + Vite SPA | Leaflet WebGIS | Lucide Icons | Responsive Glass UI   │
└────────────────────────────────────────┬─────────────────────────────────────────┘
                                         │ JSON REST APIs (HTTP / CORS)
                                         ▼
┌──────────────────────────────────────────────────────────────────────────────────┐
│                              API & ROUTING LAYER                                 │
│      FastAPI 0.110+ | Uvicorn ASGI | Pydantic v2 Validation | OpenAPI Docs       │
└────────────────────────────────────────┬─────────────────────────────────────────┘
                                         │
        ┌────────────────────────────────┴────────────────────────────────┐
        ▼                                                                 ▼
┌─────────────────────────────────────────┐   ┌────────────────────────────────────┐
│         DECISION ENGINES                │   │        DATA REPOSITORY LAYER       │
│ • MultiHazardRiskEngine                 │   │ • Hybrid Persistence:              │
│ • HabitationVulnerabilityEngine         │   │   - Supabase PostGIS (Live Spatial)│
│ • SiteSuitabilityEngine (AHP)           │   │   - Resilient In-Memory Fallback   │
│ • CarryingCapacityEngine                │   │ • GeoAlchemy2 & SQLAlchemy 2.0 ORM │
│ • PrioritizationMatrixEngine            │   │ • Alembic Database Migrations      │
│ • SimulationSandboxService              │   │                                    │
└─────────────────────────────────────────┘   └────────────────────────────────────┘
```

---

## 💻 Tech Stack

| Domain | Technology | Description |
|---|---|---|
| **Frontend UI** | **React 18, Vite** | Single-page application with modern component architecture |
| **Mapping & GIS** | **Leaflet, GeoJSON** | Interactive map layers, spatial polygon rendering, raster overlays |
| **Icons & Styling** | **Lucide React, Vanilla CSS** | Custom responsive UI with dark mode and glassmorphism accents |
| **Backend Framework** | **FastAPI, Uvicorn** | High-performance asynchronous Python API server |
| **Spatial Database** | **PostgreSQL, PostGIS** | Spatial joins, GiST indexing, distance buffers (`SRID 4326`) |
| **ORM & Persistence** | **SQLAlchemy 2.0, GeoAlchemy2** | Type-safe spatial ORM with automated repository fallback |
| **Data Science / ML** | **Shapely, NumPy, Pandas** | Geometric operations, spatial feature extraction, scoring models |
| **API Documentation** | **Swagger UI, ReDoc** | Automatic interactive API schema and documentation |

---

## 📁 Repository Directory Structure

```text
GIS-Disaster-Response-Relocation-System/
├── backend/
│   ├── app/
│   │   ├── api/v1/             # REST API routes (analytics, habitations, relocation, etc.)
│   │   ├── core/               # App configuration, settings, environment discovery
│   │   ├── db/                 # Database session, spatial models, repository layer
│   │   ├── models/             # Pydantic schemas and SQLAlchemy ORM models
│   │   ├── services/           # Risk, suitability, carrying capacity & prioritization engines
│   │   ├── utils/              # Spatial coordinate transformations and formatting helpers
│   │   └── main.py             # FastAPI entrypoint and lifespan management
│   ├── alembic/                # PostGIS database migrations
│   └── requirements.txt        # Python backend dependencies
│
├── frontend/
│   ├── src/
│   │   ├── components/         # Reusable UI modules (map, navbar, modals, cards)
│   │   ├── data/               # Domain seed datasets and fallback spatial profiles
│   │   ├── pages/              # Dashboard, RiskAnalysis, RedZones, Habitations, WhatIf
│   │   ├── services/           # API integration client with automatic resilient fallback
│   │   ├── styles/             # Application styles, tokens, and responsive layout
│   │   ├── App.jsx             # Main application layout and routing
│   │   └── main.jsx            # React root DOM mount
│   ├── package.json            # Node.js dependencies and scripts
│   └── vite.config.js          # Vite build and dev server configuration
│
├── data/                       # Spatial layers, sample DEMs, and boundary files
├── docs/                       # Architectural diagrams, specifications, and screenshots
├── BACKEND.md                  # Comprehensive backend & PostGIS architecture manual
└── README.md                   # Project overview and quickstart guide
```

---

## ⚡ Quick Start & Installation

### Prerequisites
- **Node.js**: v18.0+ (v20+ recommended)
- **Python**: v3.10+ (tested on Python 3.10–3.14)
- **Git**

---

### 1. Clone the Repository
```bash
git clone https://github.com/aryanhavkar23/GIS-Disaster-Response-Relocation-System.git
cd GIS-Disaster-Response-Relocation-System
```

---

### 2. Backend Setup (FastAPI)
```bash
# 1. Navigate to backend directory or run from root:
# (Optional) Create & activate a virtual environment
python -m venv venv

# Windows (PowerShell):
.\venv\Scripts\Activate.ps1
# Linux / macOS:
source venv/bin/activate

# 2. Install backend dependencies
pip install -r backend/requirements.txt

# 3. Start the FastAPI server
python -m uvicorn backend.app.main:app --host 127.0.0.1 --port 8000 --reload
```
- **Backend API Base:** `http://127.0.0.1:8000`
- **Interactive Swagger Docs:** `http://127.0.0.1:8000/docs`
- **ReDoc Documentation:** `http://127.0.0.1:8000/redoc`

---

### 3. Frontend Setup (React + Vite)
```bash
# In a new terminal, navigate to the frontend directory:
cd frontend

# 1. Install frontend dependencies
npm install

# 2. Start the Vite development server
npm run dev
```
- **Web Application Dashboard:** `http://localhost:5173`

---

### 4. Environment Configuration (`.env`)
A `.env.example` file is included in the project root. You can create a `.env` file to customize settings:

```ini
APP_ENV=development
APP_DEBUG=true
PORT=8000
HOST=127.0.0.1

# Spatial & Relocation Thresholds
RED_ZONE_RISK_THRESHOLD=75.0
MAX_HABITATION_SLOPE_DEGREE=15.0
MIN_CONTIGUOUS_ACRES_RELOCATION=5.0
PER_CAPITA_LAND_SQM=45.0
PER_CAPITA_WATER_LPD=135.0

# Optional Database (Supabase PostgreSQL / PostGIS)
# If omitted, system seamlessly runs in local resilient mock mode
DATABASE_URL=postgresql://user:password@localhost:5432/geodss
```

---

## 📡 Key API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/health` | System health check and runtime mode |
| `GET` | `/health/db` | PostGIS database connectivity status |
| `GET` | `/api/v1/analytics/kpis` | Summary metrics (total habitations, at-risk population, safe sites) |
| `GET` | `/api/v1/habitations/vulnerable` | List of settlements intersecting Red Zones with composite scores |
| `GET` | `/api/v1/habitations/{id}` | Detailed habitation risk breakdown & feature attribution |
| `GET` | `/api/v1/red-zones` | Demarcated multi-hazard red zone polygons and hazard tiers |
| `GET` | `/api/v1/relocation/candidate-sites` | Candidate recipient parcels with suitability scores |
| `POST` | `/api/v1/relocation/evaluate` | Evaluates carrying capacity of a candidate site for a population |
| `GET` | `/api/v1/prioritization/ranked-queue` | Algorithmic relocation priority queue (P1 to P4) |
| `POST` | `/api/v1/simulation/what-if` | Parametric policy simulation sandbox |
| `POST` | `/api/v1/reports/export-dossier` | Generates official statutory relocation action briefs |

---

## 🎯 Smart India Hackathon (SIH 2026) Demo Walkthrough

When presenting to evaluators, follow this workflow:

1. **State Command Overview**: Open `http://localhost:5173` to view the master dashboard with live KPIs across districts (Raigad, Pune, Wayanad, Idukki, Chamoli).
2. **Hazard Layers & Red Zones**: Toggle the multi-hazard layers to visualize the spatial overlap of slope gradients, floodplains, and extreme rainfall triggers.
3. **Inspect Vulnerable Habitations**: Click on a critical habitation (e.g., *Taliye Wadi*, Risk Score: `88.4 / 100`). View the Explainable AI card detailing *why* it is at risk (slope $> 32^\circ$, antecedent rainfall, single cul-de-sac road).
4. **Evaluate Candidate Relocation Sites**: Select recommended safe parcels outside the hazard boundary (e.g., *Plateau Ridge Sector 2*).
5. **Audit Carrying Capacity**: Demonstrate that the recipient site exceeds statutory thresholds ($\text{Capacity Factor} = 1.47\times$, verified water access, gentle slope $< 5^\circ$).
6. **Relocation Priority Matrix**: Review the algorithmic action queue (Immediate vs. Short-Term).
7. **Simulate Scenarios**: Use the *What-If Simulation* panel to increase rainfall anomaly by +25% and observe how the risk queue dynamically re-orders.

---

## 🤝 Contributing

Contributions are welcomed! Follow these steps:
1. **Fork the Repository**
2. **Create a Feature Branch**: `git checkout -b feature/new-spatial-layer`
3. **Commit Your Changes**: `git commit -m "feat: add watershed flow accumulation index"`
4. **Push to Branch**: `git push origin feature/new-spatial-layer`
5. **Open a Pull Request**

---

## 📜 License

This project is developed under the **Smart India Hackathon 2026** guidelines.  
Distributed under the **MIT License**. See `LICENSE` for more information.

<div align="center">
  <sub>Developed for Smart India Hackathon 2026 • Problem Statement ID 191</sub>
</div>