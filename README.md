# WattWatch Setup Guide

## Stack
Frontend: HTML/CSS/JS + Chart.js on Vercel
Backend:  Node.js + Express on Railway
Database: Supabase (PostgreSQL)

---

## Step 1 — Supabase

1. Go to https://supabase.com and create a new project
2. Open SQL Editor and run the full contents of SUPABASE_SCHEMA.sql
3. Go to Settings > API and copy:
   - Project URL
   - service_role key (under Secret)

---

## Step 2 — Backend setup

```
cd backend
npm install
```

Open .env and fill in:
```
SUPABASE_URL=https://your-project.supabase.co
SUPABASE_SERVICE_KEY=your-service-role-key
```

---

## Step 3 — Seed the hospital data

Run ONCE only:
```
node seed.js
```

This creates the sample hospital (5 floors, 8 rooms, all appliances)
and inserts 30 days of historical readings.
Note the Building ID it prints at the end.

---

## Step 4 — Update frontend

Open frontend/index.html and find line:
  const BUILDING_ID = 1;
Change 1 to whatever Building ID seed.js printed.

---

## Step 5 — Start the server

```
node server.js
```

Open http://localhost:3000

The simulation layer runs automatically every 30 seconds.
Click "Use demo account" to log in instantly.

---

## Step 6 — Deploy

Backend:  Railway (root directory = backend)
Frontend: Vercel (root directory = frontend, preset = Other)

Add .env variables to Railway dashboard.
Update const API in index.html to your Railway URL before deploying to Vercel.

---

## Pages

1. Auth       - Login / Register
2. Dashboard  - Live kW, bill, alerts, 24hr chart
3. Floor Map  - Click rooms to see appliance breakdown
4. Alerts     - Filter by type, resolve alerts, trigger demo events
5. Bill       - Tier bar, floor chart, recommended action
