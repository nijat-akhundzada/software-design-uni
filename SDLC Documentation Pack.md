# Weather Pollution Analyzer & Predictor Web Application (WPA WebApp)

**SDLC Documentation Pack**
**Version:** 1.0
**Date:** 2025-10-16

---

## Table of Contents

1. [Customer Requirements Document (CRD) Summary](#crd-summary)
2. [Software Requirements Specification (SRS) Summary](#srs-summary)
3. [SDLC Traceability Matrix](#traceability-matrix)
4. [Visual SDLC Traceability Diagram](#traceability-diagram)
5. [High-Level System Architecture](#system-architecture)
6. [Database Schema Overview](#database-schema)
7. [UML Class Diagrams](#uml-class-diagrams)
8. [Deployment & CI/CD Pipeline](#deployment-ci-cd)

---

<a name="crd-summary"></a>

## 1. Customer Requirements Document (CRD) Summary

**Project Goal:** Real-time AQI/weather insights, predictive analytics, historical trends, interactive maps, alerts & recommendations.

**Target Users:** General public, health-sensitive individuals, athletes, parents, researchers.

**Core Features:**

- Registration/Login
- Dashboard with real-time metrics
- Real-time data & pollutant breakdown
- Forecasting & historical trends
- City comparison
- Interactive AQI map
- Alerts & recommendations
- Admin management & ML model maintenance

> Full CRD: See [`WPA-CRD-002`](./WPA-CRD-002.md)

---

<a name="srs-summary"></a>

## 2. Software Requirements Specification (SRS) Summary

**Functional Modules:**

| Module               | Description                                      |
| -------------------- | ------------------------------------------------ |
| User Authentication  | Email/password login, JWT session management     |
| Dashboard            | Real-time AQI/weather metrics                    |
| Location Management  | Add/edit/delete favorite cities                  |
| Real-Time Data       | Fetch and display live AQI/weather metrics       |
| Pollutant Breakdown  | Visualize pollutant concentrations with severity |
| Forecasting          | 5–7 day predictive AQI & weather                 |
| Charts & Trends      | Interactive charts with historical data          |
| City Comparison      | Compare metrics for multiple cities              |
| Map Visualization    | Interactive map showing AQI hotspots             |
| Health Alerts        | Threshold-based notifications via email/in-app   |
| Recommendations      | Personalized health/outdoor activity advice      |
| Admin Panel          | Manage users, logs, API usage                    |
| ML Model Maintenance | Retrain & redeploy predictive ML models          |

**Non-Functional Requirements:**

- Response time: ≤ 1s
- Page load: ≤ 3s
- Uptime: ≥ 99.9%
- Scalable up to 10,000 concurrent users
- Fully responsive (mobile/desktop)
- Security: HTTPS, bcrypt, JWT, RBAC
- Accessibility: WCAG 2.1 Level AA

> Full SRS: See [`WPA-SRS-001`](./WPA-SRS-001.md)

---

<a name="traceability-matrix"></a>

## 3. SDLC Traceability Matrix

| CRD ID | SRS Feature/Module  | Functional Module     | Test Case                                                                                                 | Deployment Component                     |
| ------ | ------------------- | --------------------- | --------------------------------------------------------------------------------------------------------- | ---------------------------------------- |
| F-1.1  | User Authentication | Registration/Login    | TC-Auth-01: Register <br> TC-Auth-02: Login <br> TC-Auth-03: JWT expiry                                   | FastAPI Auth API, PostgreSQL users table |
| F-1.2  | Dashboard           | Dashboard UI          | TC-Dash-01: Display metrics <br> TC-Dash-02: Responsive layout                                            | React + Tailwind, FastAPI endpoints      |
| F-2.1  | Location Management | Location CRUD         | TC-Loc-01: Add city <br> TC-Loc-02: Edit/Delete <br> TC-Loc-03: Device location                           | React + FastAPI + PostgreSQL + Redis     |
| F-2.2  | Real-Time Data      | Data Fetching         | TC-Data-01: Fetch data <br> TC-Data-02: Validate API                                                      | FastAPI + Redis                          |
| F-2.3  | Pollutant Breakdown | Data Processing       | TC-Poll-01: Compute pollutant severity <br> TC-Poll-02: Color-coded indicators                            | FastAPI Processing Module                |
| F-3.1  | Forecasting         | ML Prediction         | TC-ML-01: Predict AQI <br> TC-ML-02: Validate accuracy                                                    | FastAPI ML API, TensorFlow/Scikit-learn  |
| F-3.2  | Interactive Charts  | Chart Rendering       | TC-Chart-01: AQI trends <br> TC-Chart-02: Hover/zoom <br> TC-Chart-03: Filter                             | Chart.js/D3.js Frontend                  |
| F-3.3  | Historical Trends   | Historical Data UI    | TC-Hist-01: Display trends <br> TC-Hist-02: Date filtering                                                | FastAPI + PostgreSQL                     |
| F-3.4  | City Comparison     | Comparison Tool       | TC-Comp-01: Select multiple cities <br> TC-Comp-02: Side-by-side metrics <br> TC-Comp-03: Validate charts | React + FastAPI                          |
| F-4.1  | Map Visualization   | Interactive Map       | TC-Map-01: AQI hotspots <br> TC-Map-02: Zoom/pan/filter                                                   | Leaflet.js/Mapbox + FastAPI Geo API      |
| F-4.2  | Health Alerts       | Alert System          | TC-Alert-01: Subscribe <br> TC-Alert-02: Receive notifications <br> TC-Alert-03: Unsubscribe              | FastAPI + Email API + DB                 |
| F-4.3  | Recommendations     | Recommendation Engine | TC-Rec-01: Generate advice <br> TC-Rec-02: Display recommendations                                        | FastAPI ML/Rule Engine                   |
| F-5.1  | Admin Management    | Admin Panel           | TC-Admin-01: Manage users <br> TC-Admin-02: Monitor logs/API                                              | React Admin UI + FastAPI                 |
| F-5.2  | Model Maintenance   | ML Model Retraining   | TC-ML-03: Retrain model <br> TC-ML-04: Redeploy <br> TC-ML-05: Validate accuracy                          | FastAPI ML API + Deployment Pipeline     |

---

<a name="traceability-diagram"></a>

## 4. Visual SDLC Traceability Diagram

```mermaid
flowchart TD
    CRD[CRD Requirements] --> SRS[SRS Features & Modules]
    SRS --> FM[Functional Modules]
    FM --> TC[Test Cases]
    TC --> DC[Deployment Components]
```

**Detailed User & Admin Feature Mapping**

```mermaid
flowchart TD
    %% User Features
    subgraph USER[User Features]
        UA[User Authentication] --> TC1[TC-Auth-01..03] --> DC1[FastAPI Auth API + PostgreSQL]
        Dash[Dashboard] --> TC2[TC-Dash-01..02] --> DC2[React + Tailwind + FastAPI]
        Loc[Location Management] --> TC3[TC-Loc-01..03] --> DC3[React + FastAPI + PostgreSQL + Redis]
        RT[Real-Time Data] --> TC4[TC-Data-01..02] --> DC4[FastAPI + Redis]
        PB[Pollutant Breakdown] --> TC5[TC-Poll-01..02] --> DC5[FastAPI Processing]
        FC[Forecasting] --> TC6[TC-ML-01..02] --> DC6[FastAPI ML API]
        CH[Charts & Trends] --> TC7[TC-Chart-01..03] --> DC7[Chart.js/D3.js]
        Hist[Historical Trends] --> TC8[TC-Hist-01..02] --> DC8[FastAPI + PostgreSQL]
        Comp[City Comparison] --> TC9[TC-Comp-01..03] --> DC9[React + FastAPI]
        Map[Map Visualization] --> TC10[TC-Map-01..03] --> DC10[Leaflet.js/Mapbox + FastAPI Geo API]
        Alerts[Health Alerts] --> TC11[TC-Alert-01..03] --> DC11[FastAPI + Email API + DB]
        Rec[Recommendations] --> TC12[TC-Rec-01..02] --> DC12[FastAPI ML/Rule Engine]
    end

    %% Admin Features
    subgraph ADMIN[Admin Features]
        Admin --> TC13[TC-Admin-01..02] --> DC13[React Admin UI + FastAPI]
        ML[Model Maintenance] --> TC14[TC-ML-03..05] --> DC14[FastAPI ML API + Deployment Pipeline]
    end
```

---

<a name="system-architecture"></a>

## 5. High-Level System Architecture

**5.1. Component Interaction Diagram**

```mermaid
flowchart LR
    Browser["React + Tailwind Frontend"] -->|HTTP/HTTPS| API["FastAPI Backend"]
    API --> DB["PostgreSQL Database"]
    API --> Cache["Redis Cache"]
    API --> ML["ML Prediction Model (TensorFlow/Scikit-learn)"]
    API --> ExtAPI["External AQI/Weather APIs"]
    ML --> API
```

**5.2. User Login and Dashboard Data Flow**

```mermaid

flowchart TD
    %% Start
    A([Start]) --> B[Open Login Page]

    %% User enters credentials
    B --> C[Enter Email & Password]
    C --> D[Click Login]

    %% Backend validation
    D --> E[FastAPI Auth API: Validate Input]
    E --> F{Credentials Valid?}

    %% Invalid case
    F -- No --> G[Show Error Message]
    G --> C

    %% Valid case
    F -- Yes --> H[Generate JWT Token]
    H --> I[Store Session / JWT in Browser]
    I --> J[Redirect to Dashboard]

    %% Dashboard Loading process
    J --> K[React loads user profile & preferences]
    K --> L[Request Favorite Locations]
    L --> M[FastAPI fetches AQI/Weather for each location]

    %% Caching logic
    M --> N{Cache Hit?}
    N -- Yes --> O[Return Cached Data]
    N -- No --> P[Fetch Live Data + ML Predictions]
    P --> Q[Store Results in DB & Redis Cache]

    %% Render UI
    O --> R[Render Dashboard Components]
    Q --> R

    R --> S([End])
```

**5.3. System Sequence Diagram**

```mermaid
sequenceDiagram
    title System Sequence Diagram
    autonumber
    actor U as User
    participant FE as React Frontend
    participant API as FastAPI Backend
    participant RC as Redis Cache
    participant EXT as External Weather API
    participant ML as ML Model Service
    participant DB as PostgreSQL DB

    Note over U, FE: TC-Loc-01: User selects a city

    U->>FE: Selects City (e.g., "Baku")
    FE->>API: GET /api/v1/weather?city=Baku

    %% Caching Strategy
    rect rgb(240, 248, 255)
        Note right of API: Caching Strategy (Performance)
        API->>RC: Check Cache for "Baku_Data"
        RC-->>API: Return Result (Hit/Miss)
    end

    alt Cache Hit (Data Exists & Fresh)
        API-->>FE: Return Cached AQI & Forecast

    else Cache Miss (Data Missing or Stale)
        par Fetch Live Data
            API->>EXT: Request Real-time AQI/Weather
            EXT-->>API: Return JSON Data
        and Get Prediction
            Note right of API: F-3.1 Forecasting
            API->>ML: Send Current Metrics
            ML-->>API: Return Predicted AQI
        end

        %% Data Persistence
        API->>DB: INSERT into AQI_DATA & FORECAST_DATA
        DB-->>API: Confirm Write

        %% Update Cache
        API->>RC: SET "Baku_Data" (Expire: 10 mins)

        API-->>FE: Return Fresh AQI & Forecast JSON
    end

    %% UI Rendering
    FE->>FE: Render Charts (Chart.js) & Maps
    FE-->>U: Display Dashboard

    %% Async Alert Check
    rect rgb(255, 240, 240)
        Note over API, DB: Background Process: F-4.2 Health Alerts
        API->>DB: Check User Alert Thresholds
        alt Threshold Exceeded
            API->>U: Send Email Notification
        end
    end


```

---

<a name="database-schema"></a>

## 6. Database Schema Overview

```mermaid
erDiagram
    USERS ||--o{ LOCATIONS : has
    USERS ||--o{ ALERTS : subscribes
    LOCATIONS ||--o{ AQI_DATA : contains
    LOCATIONS ||--o{ FORECAST_DATA : predicts

    USERS {
        int id PK
        string email
        string password_hash
        json preferences
        timestamp created_at
    }
    LOCATIONS {
        int id PK
        int user_id FK
        string city
        string coordinates
        timestamp created_at
    }
    ALERTS {
        int id PK
        int user_id FK
        int location_id FK
        int threshold
        string notification_type
    }
    AQI_DATA {
        int id PK
        string city
        timestamp timestamp
        float PM25
        float PM10
        float O3
        float CO
        float NO2
        int AQI
        float temperature
        float humidity
    }
    FORECAST_DATA {
        int id PK
        string city
        date forecast_date
        int predicted_AQI
        string predicted_weather
    }
```

---

<a name="uml-class-diagrams"></a>

## 7. UML Class Diagrams

This document contains the UML class diagrams for the Weather Pollution Analyzer & Predictor Web Application (WPA WebApp).

### Domain Model Class Diagram

This diagram illustrates the main entities of the system and their relationships.

```mermaid
classDiagram
    class User {
        +id: int
        +email: string
        +password_hash: string
        +preferences: json
        +created_at: timestamp
        +register()
        +login()
        +logout()
        +addLocation()
        +removeLocation()
        +createAlert()
        +viewDashboard()
    }

    class Admin {
        +manageUsers()
        +viewLogs()
        +retrainModel()
    }

    class Location {
        +id: int
        +user_id: int
        +city: string
        +coordinates: string
        +created_at: timestamp
        +getRealTimeData()
        +getForecast()
    }

    class Alert {
        +id: int
        +user_id: int
        +location_id: int
        +threshold: int
        +notification_type: string
        +checkThreshold()
        +sendNotification()
    }

    class AQIData {
        +id: int
        +city: string
        +timestamp: timestamp
        +pm25: float
        +pm10: float
        +o3: float
        +co: float
        +no2: float
        +aqi: int
        +temperature: float
        +humidity: float
    }

    class ForecastData {
        +id: int
        +city: string
        +forecast_date: date
        +predicted_aqi: int
        +predicted_weather: string
    }

    User <|-- Admin
    User "1" -- "0..*" Location : has
    User "1" -- "0..*" Alert : subscribes to
    Location "1" -- "0..*" AQIData : contains
    Location "1" -- "0..*" ForecastData : has
    Alert "1" -- "1" Location : for

```

### System Components and Services Diagram

This diagram shows the high-level components and services of the application and their interactions.

```mermaid
classDiagram
    class Frontend {
        +React
        +TailwindCSS
        +Chart.js / D3.js
        +Leaflet.js / Mapbox
        +renderDashboard()
        +renderCharts()
        +renderMap()
    }

    class Backend {
        +FastAPI
        +handleRequest()
        +authenticateUser()
        +getRealTimeData()
        +getForecast()
    }

    class DataFetcher {
        +fetchFromExternalAPI()
    }

    class MLModel {
        +TensorFlow / Scikit-learn
        +predictAQI()
        +predictWeather()
        +retrain()
    }

    class NotificationService {
        +sendEmail()
        +sendInAppNotification()
    }

    class Database {
        +PostgreSQL
        +Redis (Cache)
        +saveUser()
        +getAQIData()
        +cacheData()
    }

    Frontend -- Backend : Interacts via HTTP/HTTPS
    Backend -- Database : Reads/Writes
    Backend -- DataFetcher : Fetches data
    Backend -- MLModel : Gets predictions
    Backend -- NotificationService : Sends alerts
```

---

<a name="deployment-ci-cd"></a>

## 8. Deployment & CI/CD Pipeline

```mermaid
flowchart TD
    Dev[Developer] --> Git[Git Repository]
    Git --> CI["CI/CD Pipeline (GitHub Actions / GitLab CI)"]
    CI --> Test[Test Suite Execution]
    Test --> Build["Build & Containerize (Docker)"]
    Build --> Deploy["Deploy to Cloud (AWS/GCP/Azure)"]
    Deploy --> Monitor["Monitoring & Logging (Prometheus/Grafana)"]
    Monitor --> Dev

```

**Deployment Notes:**

- Backend and ML services containerized with **Docker**
- Frontend deployed to **CDN / Static Hosting**
- CI/CD automates **test → build → deploy**
- Monitoring ensures uptime, API health, and alert delivery

---
