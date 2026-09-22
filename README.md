# 🚜 CatRent Intelligence

> **“We don't just tell the rental manager where equipment is. We tell them where it should be next.”**

**CatRent Intelligence** is an industrial fleet intelligence platform designed for construction and mining equipment rental operations.

The platform combines **real-time equipment tracking, telemetry, anomaly detection, demand forecasting, fleet utilization analysis, redeployment recommendations, and an AI Operations Copilot** to help rental managers make faster and data-driven decisions.

Built as part of a **Caterpillar Hackathon**.

---

## 🎯 Problem Statement

Construction and mining rental fleets generate large amounts of operational data, but rental managers often need to make decisions using fragmented information.

Common challenges include:

* Equipment sitting idle at low-utilization sites
* Difficulty tracking equipment movement
* Delayed identification of abnormal equipment behavior
* Unpredictable rental demand
* Poor visibility into fleet utilization
* Manual redeployment decisions
* Difficulty identifying overdue or underperforming assets

CatRent Intelligence aims to transform this operational data into **actionable fleet intelligence**.

---

## 💡 Proposed Solution

CatRent Intelligence is designed around five major capabilities:

### 1. 📍 Fleet Tracking

Track equipment across rental sites and locations with real-time or simulated telemetry.

### 2. 🚨 Anomaly Detection

Identify unusual equipment behavior and operational patterns using machine learning.

Examples include:

* Abnormally low utilization
* Excessive idle time
* Unusual rental duration
* Unexpected equipment activity

### 3. 📈 Demand Forecasting

Forecast future equipment demand using historical rental and utilization data.

This can help rental managers anticipate:

* High-demand equipment
* Future site requirements
* Potential shortages
* Opportunities for redeployment

### 4. 🔄 Redeployment Recommendations

Recommend where equipment should be moved next based on:

* Current location
* Utilization
* Equipment availability
* Rental demand
* Forecasted requirements

### 5. 🤖 AI Operations Copilot

An AI-powered operational assistant designed to help rental managers interact with fleet data using natural language.

Example queries:

```text
Which equipment has been idle for more than 7 days?

Which machines should we redeploy next month?

Why is equipment EQX1002 underperforming?

Which sites are likely to need additional excavators?
```

---

# 🏗️ System Architecture

```text
                    ┌──────────────────────┐
                    │      React UI         │
                    │  TypeScript + Vite    │
                    └──────────┬───────────┘
                               │
                         REST / WebSocket
                               │
                               ▼
                    ┌──────────────────────┐
                    │    Node.js Backend   │
                    │ Express + TypeScript  │
                    └───────┬───────┬──────┘
                            │       │
                     MongoDB       │
                            │       │
                            ▼       ▼
                    ┌──────────┐  ┌──────────────┐
                    │ MongoDB  │  │  ML Service  │
                    │ Database │  │   FastAPI    │
                    └──────────┘  └──────┬───────┘
                                         │
                                         ▼
                              ┌────────────────────┐
                              │ Python ML Pipeline │
                              │ pandas / NumPy     │
                              │ scikit-learn       │
                              └────────────────────┘
```

---

# 🛠️ Technology Stack

## Frontend

* React
* TypeScript
* Vite
* Tailwind CSS
* shadcn/ui
* React Query
* Zustand
* Recharts
* Leaflet

## Backend

* Node.js
* Express.js
* TypeScript
* Mongoose
* Socket.IO
* JWT Authentication
* bcrypt

## Machine Learning

* Python
* FastAPI
* pandas
* NumPy
* scikit-learn

Planned ML capabilities include:

* Anomaly Detection
* Demand Forecasting
* Equipment Utilization Analysis
* Redeployment Recommendations

## Database

* MongoDB

## Testing

* Jest
* Supertest
* Vitest
* React Testing Library
* pytest

## DevOps / Infrastructure

* Docker
* Docker Compose
* Git
* GitHub

---

# 📂 Project Structure

```text
catrent-intelligence/
│
├── backend/
│   ├── src/
│   │   ├── config/
│   │   ├── controllers/
│   │   ├── middleware/
│   │   ├── models/
│   │   ├── routes/
│   │   ├── services/
│   │   ├── jobs/
│   │   ├── sockets/
│   │   └── utils/
│   └── package.json
│
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── hooks/
│   │   ├── services/
│   │   ├── store/
│   │   ├── types/
│   │   └── utils/
│   └── package.json
│
├── ml-service/
│   ├── app/
│   │   ├── forecasting/
│   │   ├── anomaly/
│   │   └── recommendations/
│   └── requirements.txt
│
├── data/
│   └── synthetic/
│
├── docs/
│
├── docker-compose.yml
├── .env.example
├── .gitignore
├── LICENSE
└── README.md
```

---

# 🚀 Getting Started

## Prerequisites

Make sure you have the following installed:

* Node.js 18+
* npm
* Python 3.10+
* MongoDB or MongoDB Atlas
* Docker Desktop *(recommended)*

---

## 🐳 Option 1 — Docker Compose

The recommended setup is Docker Compose.

### 1. Clone the repository

```bash
git clone https://github.com/babjanshaik-png/catrent.git
cd catrent
```

### 2. Create environment variables

```bash
cp .env.example .env
```

On Windows PowerShell:

```powershell
Copy-Item .env.example .env
```

Configure the required values, especially:

```env
JWT_SECRET=your_secure_secret
MONGO_URI=your_mongodb_connection_string
```

### 3. Start the application

```bash
docker compose up --build
```

### Services

| Service        | URL                                |
| -------------- | ---------------------------------- |
| Frontend       | `http://localhost:5173`            |
| Backend        | `http://localhost:4000`            |
| Backend Health | `http://localhost:4000/api/health` |
| ML Service     | `http://localhost:8000`            |
| ML Health      | `http://localhost:8000/health`     |
| MongoDB        | `localhost:27017`                  |

---

# 💻 Option 2 — Run Services Locally

## Backend

```bash
cd backend
npm install
```

Create your environment file:

```bash
cp ../.env.example .env
```

Configure MongoDB and JWT settings.

Then:

```bash
npm run build
npm start
```

For development:

```bash
npm run dev
```

Backend health check:

```text
http://localhost:4000/api/health
```

Expected response:

```json
{
  "status": "ok"
}
```

---

## Frontend

Open another terminal:

```bash
cd frontend
npm install
npm run dev
```

Open:

```text
http://localhost:5173
```

The frontend communicates with the backend health endpoint and displays service connectivity status.

---

## ML Service

Open another terminal:

```bash
cd ml-service
pip install -r requirements.txt
```

Start FastAPI:

```bash
uvicorn app.main:app --reload
```

ML service health check:

```text
http://localhost:8000/health
```

Expected response:

```json
{
  "status": "ok",
  "service": "catrent-ml-service"
}
```

---

# 🧪 Testing

## Backend

```bash
cd backend
npm test
```

## Frontend

```bash
cd frontend
npm test
```

## ML Service

```bash
cd ml-service
pytest
```

---

# ✅ Phase 2 Verification

| Check                   | Backend | Frontend | ML Service |
| ----------------------- | :-----: | :------: | :--------: |
| Dependencies install    |    ✅    |     ✅    |      ✅     |
| Type checking           |    ✅    |     ✅    |     N/A    |
| Unit tests              |  ✅ 2/2  |   ✅ 2/2  |    ✅ 1/1   |
| Production build        |    ✅    |     ✅    |     N/A    |
| HTTP health check       |    ✅    |     ✅    |     ⚠️     |
| Docker Compose          |    ⏳    |     ⏳    |      ⏳     |
| Real MongoDB connection |    ⏳    |    N/A   |     N/A    |

The initial foundation was verified without Docker or a running MongoDB daemon in the development environment.

The next local verification step is:

```bash
docker compose up --build
```

and confirming that the backend reports:

```json
"dbConnected": true
```

when connected to a valid MongoDB instance.

---

# 🗺️ Development Roadmap

The project is planned across multiple development phases.

### Phase 1 — Architecture

* System architecture
* Service boundaries
* Technology selection

### Phase 2 — Foundation ✅

* Frontend scaffolding
* Backend scaffolding
* ML service scaffolding
* Testing setup
* Docker configuration

### Phase 3 — Data

* Mongoose schemas
* Equipment model
* Rental model
* Site model
* Operator model
* Telemetry model
* Synthetic dataset

### Phase 4 — Core APIs

* Equipment CRUD
* Rental APIs
* Site management
* Authentication
* Authorization

### Phase 5 — Fleet Dashboard

* KPI dashboard
* Equipment status
* Utilization metrics
* Fleet overview

### Phase 6 — Real-Time Tracking

* Telemetry simulation
* Socket.IO
* Live equipment map
* Equipment movement

### Phase 7 — Anomaly Detection

* Feature engineering
* Isolation Forest
* Anomaly scoring
* Explainable anomaly reasons

### Phase 8 — Demand Forecasting

* Historical demand analysis
* Forecasting pipeline
* Future equipment demand

### Phase 9 — Redeployment Engine

* Equipment matching
* Site demand matching
* Redeployment recommendations

### Phase 10 — AI Operations Copilot

* Natural-language fleet queries
* Operational insights
* AI-generated recommendations

### Phase 11 — Simulation & Optimization

* What-if scenarios
* Fleet optimization
* Utilization improvements

### Phase 12 — Demo & Deployment

* End-to-end integration
* Production deployment
* Documentation
* Hackathon demo

---

# 🔐 Security

The platform is designed with security considerations including:

* JWT-based authentication
* Password hashing using bcrypt
* Environment-based secrets
* Role-based access control
* API validation
* Protected backend routes

> Never commit real secrets, API keys, database credentials, or `.env` files to GitHub.

---

# 📊 Future Capabilities

The completed platform is intended to provide:

```text
Fleet Data
     │
     ▼
Real-Time Monitoring
     │
     ├── Utilization Analysis
     │
     ├── Anomaly Detection
     │
     ├── Demand Forecasting
     │
     └── Equipment Recommendations
                    │
                    ▼
             AI Operations
                Copilot
                    │
                    ▼
            Better Fleet Decisions
```

---

# 🤝 Contributing

Contributions, suggestions, and improvements are welcome.

1. Fork the repository
2. Create a feature branch

```bash
git checkout -b feature/your-feature
```

3. Commit your changes

```bash
git commit -m "Add your feature"
```

4. Push the branch

```bash
git push origin feature/your-feature
```

5. Open a Pull Request

---

# 📄 License

This project is licensed under the **MIT License**.

See the [`LICENSE`](LICENSE) file for details.

---

# 👨‍💻 Author

**Shaik Babjan**

Computer Science Engineering

📧 Email: `babjanshaik712@gmail.com`

GitHub: `https://github.com/babjanshaik-png`

---

