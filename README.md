# Log Ingestion and Querying System

This is a full-stack log ingestion and querying system built for the **Evallo.ai Technical Assessment**.  
It features a **Node.js + Express** backend with REST APIs and a **React 19.1.0** frontend (powered by **Vite 7.0.0**). Logs are persisted in a JSON file instead of a database.

---

## 🚀 Project Overview

The system provides:

- **Log Ingestion:**  
  Accepts logs via `POST /api/logs` with validated fields (`level`, `message`, `timestamp`, etc.).

- **Log Querying:**  
  Filters logs via `GET /api/logs` using criteria like `level`, `message`, `resourceId`, and `timestamp` range.

- **Frontend Interface:**  
  A responsive UI with:
  - A filter form with search functionality
  - A table displaying logs with **colored borders** indicating log levels

---

## 📁 Project Structure

log-system/
├── backend/
│ ├── src/
│ │ ├── routes/
│ │ │ └── logs.js # API routes for log ingestion and querying
│ │ ├── utils/
│ │ │ └── fileStorage.js # JSON file read/write operations
│ │ └── index.js # Main server file
│ ├── logs.json # Log storage file
│ └── package.json # Backend dependencies and scripts
├── frontend/
│ ├── src/
│ │ ├── components/
│ │ │ ├── LogFilter.jsx # Filter form with search button
│ │ │ └── LogTable.jsx # Log display table
│ │ ├── utils/
│ │ │ └── api.js # API fetch logic
│ │ ├── App.jsx # Main React component
│ │ ├── App.css # Styling for App
│ │ ├── index.css # Global styles
│ │ ├── main.jsx # Frontend entry point
│ │ └── assets/
│ │ └── react.svg # Vite-generated asset
│ ├── public/
│ │ └── vite.svg # Vite-generated asset
│ ├── eslint.config.js # ESLint configuration
│ ├── index.html # HTML entry point
│ ├── package.json # Frontend dependencies and scripts
│ └── vite.config.js # Vite configuration
└── README.md # Project documentation (this file)

yaml
Copy
Edit



---

## ⚙️ Setup Instructions

### ✅ Prerequisites

- **Node.js:** v22.17.0 (or v16+)
- **npm:** v10.9.2 (or compatible)

---

### 🔧 Backend Setup

```bash
cd backend
npm install
npm start


### 💻 Frontend Setup

cd frontend
npm install
npm run dev

Runs on http://localhost:5173
If port is in use:

set PORT=5174 && npm run dev

🧪 Usage
Ingest Logs (POST)

curl -X POST http://localhost:5000/api/logs \
-H "Content-Type: application/json" \
-d '{"level":"error","message":"Test error","timestamp":"2025-07-03T12:00:00.000Z","resourceId":"server-1"}'

Required fields:
level (one of: error, warning, info)
message, timestamp (ISO 8601 format)

Optional fields:
resourceId, traceId, spanId, commit, metadata

Query Logs (GET)
Open http://localhost:5173

Use the filter form:

Select level (info, warning, error)

Input text for message or resourceId

Choose timestamp range

Click Search

View results in a table:

Red border = error

Yellow border = warning

Blue border = info

🧠 Design Decisions
Backend
Express: For scalable REST APIs

fs.promises: JSON file storage (no DB)

Input validation:

Valid level

Valid timestamp (ISO 8601)

In-memory filtering for fast access (good for small data sets)

Frontend
React 19.1.0 with Vite 7.0.0 for blazing fast DX

Functional Components using useState

Explicit Search button as per assessment requirements

Minimal custom CSS with visual indicators for log levels

Error Handling
Backend:

400 Bad Request for invalid inputs

500 Internal Server Error for file failures

Frontend:

Loading indicator

Logs errors to console

⚖️ Trade-offs
Decision	Trade-off
JSON file storage	Easy to implement, not scalable for large data
No pagination	Simplicity; faster development
No CSS framework	Lightweight, less dependencies
In-memory filtering	Fast for small data, not suitable for large-scale systems

🌟 Bonus Features
Loading spinner during fetch

Input validation and robust error handling

Colored borders to visually represent log levels

📝 Notes
If logs.json does not exist, it is auto-initialized as an empty array []

Backend enforces:

Valid level: error, warning, info

Valid timestamp: ISO 8601

Logs are displayed in reverse chronological order on the frontend


## 🧪 Log Previews by Type

#### 🗂️ All Logs
![All Logs](./frontend/public/images/all-logs.png)

#### 🔴 Error Logs
![Error Logs](./frontend/public/images/error-logs.png)

#### 🟡 Warning Logs
![Warning Logs](./frontend/public/images/warning-logs.png)

#### 🔵 Info Logs
![Info Logs](./frontend/public/images/info-logs.png)



