``` mermaid
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