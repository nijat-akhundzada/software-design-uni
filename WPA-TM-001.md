# WPA WebApp SDLC Traceability Matrix

**Project:** Weather Pollution Analyzer and Predictor Web Application
**Document ID:** WPA-TM-001
**Version:** 1.0
**Date:** 2025-10-16

---

| **CRD ID** | **SRS Feature/Module** | **Functional Module** | **Test Case**                                                                                                                   | **Deployment Component**                                      |
| ---------- | ---------------------- | --------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- |
| F-1.1      | User Authentication    | Registration/Login    | TC-Auth-01: Register user with email/password <br> TC-Auth-02: Login with valid credentials <br> TC-Auth-03: JWT session expiry | Backend: FastAPI Auth API <br> DB: PostgreSQL users table     |
| F-1.2      | User Dashboard         | Dashboard UI          | TC-Dash-01: Display current AQI/Weather metrics <br> TC-Dash-02: Verify responsive layout on desktop/mobile                     | Frontend: React + Tailwind <br> Backend: FastAPI endpoints    |
| F-2.1      | Location Management    | Location CRUD         | TC-Loc-01: Add favorite city <br> TC-Loc-02: Edit location <br> TC-Loc-03: Delete location <br> TC-Loc-04: Use device location  | Frontend: Location form/UI <br> Backend: PostgreSQL + FastAPI |
| F-2.2      | Real-Time Data         | Data Fetching         | TC-Data-01: Fetch real-time AQI/weather <br> TC-Data-02: Validate data consistency with API                                     | Backend: FastAPI <br> Cache: Redis                            |
| F-2.3      | Pollutant Breakdown    | Data Processing       | TC-Poll-01: Correctly compute pollutant concentration severity <br> TC-Poll-02: Display color-coded indicators                  | Backend: FastAPI + Data processing module                     |
| F-3.1      | Forecasting            | ML Prediction         | TC-ML-01: Predict AQI for next 5–7 days <br> TC-ML-02: Forecast matches expected accuracy (R² ≥ 0.85)                           | Backend: FastAPI ML API <br> Model: TensorFlow/Scikit-learn   |
| F-3.2      | Interactive Charts     | Chart Rendering       | TC-Chart-01: Render AQI trends <br> TC-Chart-02: Hover and zoom interactivity <br> TC-Chart-03: Filter by pollutant             | Frontend: Chart.js/D3.js                                      |
| F-3.3      | Historical Trends      | Historical Data UI    | TC-Hist-01: Display AQI trends over weeks/months <br> TC-Hist-02: Ensure correct date filtering                                 | Backend: FastAPI <br> DB: PostgreSQL                          |
| F-3.4      | City Comparison        | Comparison Tool       | TC-Comp-01: Select multiple cities <br> TC-Comp-02: Display metrics side by side <br> TC-Comp-03: Validate chart correctness    | Frontend: React UI <br> Backend: FastAPI                      |
| F-4.1      | Map Visualization      | Interactive Map       | TC-Map-01: Display AQI map with hotspots <br> TC-Map-02: Zoom/pan functionality <br> TC-Map-03: Filter by city or pollutant     | Frontend: Leaflet.js/Mapbox <br> Backend: FastAPI Geo API     |
| F-4.2      | Health Alerts          | Alert System          | TC-Alert-01: Subscribe to AQI threshold <br> TC-Alert-02: Receive email/in-app notification <br> TC-Alert-03: Unsubscribe       | Backend: FastAPI + Email API <br> DB: alerts table            |
| F-4.3      | Recommendations        | Recommendation Engine | TC-Rec-01: Generate health advice based on AQI <br> TC-Rec-02: Display personalized recommendations                             | Backend: FastAPI ML/Rule Engine                               |
| F-5.1      | Admin Management       | Admin Panel           | TC-Admin-01: View user list <br> TC-Admin-02: Manage alerts <br> TC-Admin-03: Monitor API usage/logs                            | Frontend: React admin UI <br> Backend: FastAPI                |
| F-5.2      | Model Maintenance      | ML Model Retraining   | TC-ML-02: Retrain model with new data <br> TC-ML-03: Redeploy without downtime <br> TC-ML-04: Validate prediction accuracy      | Backend: FastAPI ML API <br> Deployment pipeline              |

---

### Notes:

1. **Test Case Naming Convention:** `TC-<Module>-<Number>` ensures each functionality can be tested and traced.
2. **Deployment Components:** Includes both backend, frontend, and database/cache dependencies for SDLC traceability.
3. This table ensures **end-to-end coverage** from CRD requirements → implementation → testing → deployment.
