# Inventory Optimizer
### Smart Inventory Management Through Predictive Analytics

**React | Python | FastAPI | Machine Learning | SQLite | PostgreSQL | Redis**

---

## Project Overview

Managing inventory is more than keeping track of products on shelves. Businesses need to know what is selling, how quickly stock is moving, when to replenish supplies, and how to avoid unnecessary stockholding costs.

**Inventory Optimizer** is a web-based inventory management and demand forecasting system developed to address these challenges.

The application brings together real-time stock monitoring, sales tracking, demand forecasting, and intelligent reorder recommendations in one dashboard.

Rather than relying entirely on manual calculations or guesswork, the system uses historical sales information and Long Short-Term Memory (LSTM) forecasting to help estimate future product demand.

The goal is straightforward: **help businesses maintain the right stock levels, reduce shortages, minimize excess inventory, and make better purchasing decisions.**

## The Problem

Poor inventory planning can affect both business profitability and customer satisfaction.

Some of the common challenges include:

- **Stock shortages:** Popular products run out before replacements arrive.
- **Overstocking:** Slow-moving products occupy storage space and tie up working capital.
- **Unreliable demand estimates:** Purchasing decisions are made without adequate sales analysis.
- **Limited visibility:** Business owners struggle to monitor stock movement and identify products that need attention.
- **Delayed replenishment:** Orders are placed too late, resulting in interrupted product availability.

Inventory Optimizer addresses these problems by combining inventory records with demand predictions and practical stock replenishment tools.

## Project Objectives

The system was developed with the following objectives:

1. Provide a centralized platform for monitoring inventory levels.
2. Analyze historical sales patterns to support demand forecasting.
3. Use LSTM deep learning models to estimate future product demand.
4. Identify products that may require replenishment.
5. Track pending stock orders and expected delivery dates.
6. Improve visibility into sales performance and inventory movement.
7. Support informed purchasing and stock management decisions.

## Core Features

### 1. Inventory Dashboard

The dashboard provides a clear overview of available stock and product performance.

Users can monitor inventory quantities, review product information, and quickly identify products requiring attention.

### 2. Demand Forecasting

The system uses a Long Short-Term Memory (LSTM) model to generate demand forecasts from historical sales data.

Forecast results are presented through an interactive graph, making it easier to understand expected changes in product demand.

### 3. Stock Reorder Recommendations

Products that require replenishment are identified through the **REORDER** status.

Selecting this status allows the user to enter an order quantity and expected arrival date.

Pending orders remain separate from available stock until they are received.

### 4. Projected Stock Balance

The projected stock-balance chart brings together three important factors:

- Current stock on hand.
- Forecast product demand.
- Expected arrivals of pending deliveries.

This helps users understand how stock availability may change over time.

### 5. Sales Recording

Sales can be recorded directly from the dashboard.

Each product has a selling price expressed in Kenyan shillings (KES). For demo products, this price is randomly assigned once.

When a user enters the quantity sold, the application automatically calculates the total sale amount.

### 6. Sales History

A recent sales table provides a record of transactions, including quantities, timestamps, and sale amounts.

This makes it easier to review sales activity and monitor product movement.

### 7. Forecast Performance Indicators

The dashboard includes recent demand trends and forecast accuracy indicators.

These provide additional context for interpreting predictions and evaluating demand patterns.

### 8. Delivery and Order Management

Users can record expected deliveries and update order status when goods arrive.

Once an order is marked as received, the delivered quantity is added to the available inventory.

This ensures that stock calculations distinguish between goods already available and goods still in transit.

## Technology Stack

| Component | Technology |
|---|---|
| Frontend | React, JavaScript, Vite |
| Backend | Python, FastAPI |
| Default database | SQLite |
| Optional database | PostgreSQL |
| Demand forecasting | LSTM Deep Learning |
| Optional caching | Redis |
| API documentation | Swagger UI |
| Development environment | Visual Studio Code |
| Optional service management | Docker Compose |

## System Architecture

The application follows a frontend-backend architecture.

**Frontend — React**

Provides the user interface, dashboard charts, sales recording forms, and inventory management views.

**Backend — FastAPI**

Processes requests, manages inventory operations, records transactions, and provides forecasting results through API endpoints.

**Database — SQLite or PostgreSQL**

Stores inventory information, sales records, product prices, and order-related data.

**Forecasting — LSTM**

Uses historical demand information to estimate future product requirements.

**Caching — Redis**

Can be used to cache forecast results. If Redis is unavailable, the application falls back to an in-process forecast cache.

## System Requirements

Before running the project, install the following:

- Python 3.10–3.12
- Node.js 18 or later
- npm
- Visual Studio Code or another suitable code editor

**Optional:** Docker, PostgreSQL, and Redis.

SQLite is used by default, so a separate database server is not necessary for local development.

## Installation and Setup

The following instructions are intended for Windows using PowerShell.

Open two PowerShell terminals in the project directory: one for the backend and another for the frontend.

### Step 1: Set Up the Backend

Navigate to the backend directory:

```powershell
cd backend
```

Create a Python virtual environment:

```powershell
python -m venv .venv
```

Activate the environment:

```powershell
.\.venv\Scripts\Activate.ps1
```

Install the required Python packages:

```powershell
python -m pip install -r requirements.txt
```

Create the environment configuration file if it does not already exist:

```powershell
if (!(Test-Path .env)) { Copy-Item .env.example .env }
```

Prepare the demo database:

```powershell
python seed.py
```

Start the FastAPI server:

```powershell
python -m uvicorn app.main:app --reload --host 127.0.0.1 --port 8000
```

The backend will be available at:

http://127.0.0.1:8000

Interactive API documentation:

http://127.0.0.1:8000/docs

### Step 2: Set Up the Frontend

In the second PowerShell terminal, navigate to the frontend directory:

```powershell
cd frontend
```

Install the required dependencies:

```powershell
npm install
```

Start the React development server:

```powershell
npm run dev -- --host 127.0.0.1
```

Open the dashboard in your browser:

**http://127.0.0.1:5173**

You can also access it using http://localhost:5173.

Vite automatically forwards `/api` requests to the backend during local development.

## Running the Complete Application

The frontend can also be built and served directly through FastAPI, allowing the application to operate from a single origin.

Build the React frontend:

```powershell
cd frontend
npm install
npm run build
```

Return to the backend directory:

```powershell
cd ..\backend
```

Activate the Python environment:

```powershell
.\.venv\Scripts\Activate.ps1
```

Start the application:

```powershell
python -m uvicorn app.main:app --host 127.0.0.1 --port 8000
```

Open:

**http://127.0.0.1:8000**

When the `frontend\dist` directory exists, FastAPI serves the compiled frontend.

For separate frontend and backend deployments, configure `VITE_API_URL` with the API's `/api` base URL before building the frontend.

## Database Management

### SQLite

SQLite is the default database and is stored at:

`backend\inventory.db`

The database path is resolved relative to the backend directory, regardless of where the API is started.

When an existing database is detected, startup adds the required price and timestamp fields without deleting existing inventory or sales records.

Older sales records are assigned their previously recorded date at midnight.

### Demo Data

To populate the application with sample inventory information:

```powershell
python seed.py
```

Running this command does not overwrite an existing inventory.

To intentionally reset the database and replace inventory and sales records with fresh demonstration data:

```powershell
python seed.py --reset
```

**Warning:** The reset operation replaces existing inventory and sales data. Use it only when that is intended.

### PostgreSQL

PostgreSQL can be used as an alternative to SQLite.

Start the optional services:

```powershell
docker compose up -d
```

Set the database connection string in the backend environment:

```powershell
$env:DATABASE_URL = "postgresql://postgres:postgres@localhost:5432/inventory"
```

The example credentials are intended for local development and should be changed for any shared deployment.

## Redis and Forecast Caching

Redis is supported as an optional caching service.

Caching helps avoid unnecessary repeated forecast calculations when the same results are requested.

If Redis is not running, the application continues using an in-process forecast cache.

The dashboard displays Redis availability, allowing users to check its status.

## How the System Works

A typical inventory management workflow involves the following stages:

**1. Inventory monitoring**

The system displays available products and their current stock quantities.

**2. Sales recording**

A user records a sale, and the application updates the relevant inventory and transaction records.

**3. Demand analysis**

Historical sales information provides the basis for analyzing product demand.

**4. Forecast generation**

The LSTM forecasting component estimates future demand using available historical information.

**5. Replenishment planning**

Users review reorder recommendations and record quantities and expected delivery dates.

**6. Stock receiving**

When ordered products arrive, the user marks the order as received. The delivered quantity is then added to available stock.

This workflow connects daily sales activity with future inventory planning.

## Security Considerations

The current application is designed for trusted local development and demonstration environments.

**Authentication and user authorization are not implemented.**

Anyone who can access the application can view inventory information and record sales.

For this reason, the application should only be used on a trusted local machine or network. It should not be exposed directly to the public internet or an untrusted network.

A production deployment would require additional safeguards, including user authentication, role-based access control, secure configuration, and appropriate network protection.

## Project Data and Limitations

The included sample inventory and sales records are synthetic and intended for demonstration.

Forecast quality depends on the amount, consistency, and relevance of the available historical sales data. Predictions should therefore be treated as planning estimates rather than guaranteed future demand.

The project ZIP intentionally excludes local configuration files, database files, virtual environments, and installed dependency folders.

## Future Improvements

Potential areas for further development include:

- Secure user login and role-based permissions.
- Supplier management and purchase order tracking.
- Barcode scanning and point-of-sale integration.
- Low-stock notifications and automated alerts.
- Additional forecasting models for performance comparison.
- Automated inventory optimization based on holding costs, lead times, and service levels.
- Exportable inventory, sales, and forecasting reports.
- Multi-branch inventory management.

These improvements would help extend the system from a local demonstration application into a more comprehensive business inventory management platform.

## Conclusion

Inventory Optimizer demonstrates how modern web technologies and predictive analytics can work together to improve inventory management.

By connecting sales records, stock monitoring, demand forecasts, and replenishment planning, the project provides a practical foundation for data-driven inventory decisions.

Its main value lies in turning everyday inventory records into useful information that can support better stock planning, reduce unnecessary purchases, and improve product availability.

---

**Inventory Optimizer — Better Stock Planning Through Data.**
