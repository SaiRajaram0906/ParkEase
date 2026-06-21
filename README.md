# 🅿️ ParkEase India
> A JustPark-style parking space booking platform built for Indian cities.
ParkEase India lets drivers find, book, and review parking spots across major Indian cities — while giving space owners a dashboard to list and manage their spots.
---
## ✨ Features
- 🔍 **Browse & Search** parking spots by city, vehicle type, price, and availability
- 📅 **Book by Hour or Day** with INR pricing
- 📋 **Booking Management** — track, confirm, cancel, and complete bookings
- 🅿️ **Spot Detail Pages** with reviews and a quick booking form
- 🏠 **Owner Dashboard** — list and manage parking spots
- 📊 **Admin Dashboard** — stats, city breakdown chart (Recharts), top spots
- 👤 **User Profiles** for drivers and parking space owners
- 🗺️ **Google Maps Integration** for spot location display
---
## 🛣️ Pages
|
 Route 
|
 Description 
|
|
-------
|
-------------
|
|
`/`
|
 Home / Landing — search by city, featured spots 
|
|
`/spots`
|
 Browse spots with filters (city, vehicle type, price) 
|
|
`/spots/:id`
|
 Spot detail, reviews, and booking form 
|
|
`/bookings`
|
 My Bookings list 
|
|
`/bookings/:id`
|
 Booking detail with cancel option 
|
|
`/dashboard`
|
 Owner / admin dashboard with stats and charts 
|
|
`/profile`
|
 User profile and settings 
|
|
`/list-spot`
|
 Form to list your parking spot 
|
---
## 🏗️ Tech Stack
### Monorepo
|
 Tool 
|
 Version 
|
|
------
|
---------
|
|
 Package Manager 
|
 pnpm workspaces 
|
|
 Node.js 
|
 24 
|
|
 TypeScript 
|
 ~5.9 
|
### Frontend (`/frontend`)
|
 Technology 
|
 Purpose 
|
|
------------
|
---------
|
|
 React 
|
 UI framework 
|
|
 Vite 
|
 Dev server & bundler 
|
|
 TailwindCSS v4 
|
 Styling 
|
|
 Wouter 
|
 Client-side routing 
|
|
 TanStack Query 
|
 Server state management 
|
|
 Recharts 
|
 Dashboard charts 
|
|
 Framer Motion 
|
 Animations 
|
|
 Radix UI 
|
 Accessible component primitives 
|
|
 React Hook Form + Zod 
|
 Form validation 
|
|
 Leaflet / Google Maps 
|
 Map display 
|
|
 Lucide React 
|
 Icons 
|
### Backend (`/backend`)
|
 Technology 
|
 Purpose 
|
|
------------
|
---------
|
|
 Express 5 
|
 HTTP API server 
|
|
 Drizzle ORM 
|
 Database ORM 
|
|
 PostgreSQL 
|
 Relational database 
|
|
 Zod 
|
 Request/response validation 
|
|
 Pino 
|
 Structured logging 
|
|
 esbuild 
|
 Build bundler (CJS) 
|
### Shared Libraries (`/lib`)
|
 Package 
|
 Purpose 
|
|
---------
|
---------
|
|
`@workspace/db`
|
 Drizzle schema + database client 
|
|
`@workspace/api-spec`
|
 OpenAPI specification 
|
|
`@workspace/api-zod`
|
 Zod schemas generated from OpenAPI 
|
|
`@workspace/api-client-react`
|
 React Query hooks (generated via Orval) 
|
---
## 📦 Project Structure
```
├── frontend/          # React + Vite frontend app
│   └── src/
│       ├── pages/     # Route-level page components
│       ├── components/# Reusable UI components
│       ├── hooks/     # Custom React hooks
│       ├── context/   # React context providers
│       └── lib/       # Utilities
├── backend/           # Express 5 API server
│   └── src/
│       ├── routes/    # API route handlers (spots, bookings, users, reviews, dashboard)
│       ├── middlewares/
│       └── lib/
├── lib/               # Shared workspace packages
│   ├── db/            # Drizzle ORM schema & migrations
│   ├── api-spec/      # OpenAPI spec
│   ├── api-zod/       # Generated Zod validators
│   └── api-client-react/ # Generated React Query hooks
├── package.json       # Workspace root
└── pnpm-workspace.yaml
```
---
## 🗃️ Database Schema
|
 Table 
|
 Fields 
|
|
-------
|
--------
|
|
`users`
|
 name, email, phone, role (
`driver`
 / 
`owner`
 / 
`admin`
) 
|
|
`spots`
|
 title, location, city, price, vehicle type, availability 
|
|
`bookings`
|
 user, spot, vehicle, start/end time, payment status 
|
|
`reviews`
|
 user, spot, star rating, comment 
|
### Seed Data (included)
- 5 Indian users (2 owners, 2 drivers, 1 admin)
- 8 parking spots across Mumbai, Delhi, Bengaluru, Hyderabad, Pune, Chennai, Gurugram
- 6 sample bookings (mix of completed and upcoming)
- 6 reviews linked to spots
---
## 🚀 Getting Started
### Prerequisites
- [Node.js 24+](https://nodejs.org/)
- [pnpm](https://pnpm.io/installation) (`npm install -g pnpm`)
- [PostgreSQL 15+](https://www.postgresql.org/download/) running locally
### 1. Clone the repository
```bash
git clone https://github.com/muthu00712/ParkEase.git
cd ParkEase
```
### 2. Install dependencies
```bash
pnpm install
```
### 3. Set up environment variables
**Backend** — create `backend/.env`:
```env
DATABASE_URL="postgresql://postgres:your_password@localhost:5432/parkease"
PORT=5000
```
**Frontend** — create `frontend/.env`:
```env
VITE_GOOGLE_MAPS_API_KEY=your_google_maps_api_key
```
### 4. Set up the database
```bash
# Create the parkease database in PostgreSQL first, then push the schema:
pnpm --filter @workspace/db run push
```
### 5. Run the development servers
**Start the backend API server (port 5000):**
```bash
pnpm --filter @workspace/api-server run dev
```
**Start the frontend dev server (port 5173):**
```bash
pnpm --filter @workspace/parkease run dev
```
Then open **[http://localhost:5173](http://localhost:5173)** in your browser.
> The frontend automatically proxies `/api` requests to the backend at `http://localhost:5000`.
---
## 🔧 Available Scripts
|
 Command 
|
 Description 
|
|
---------
|
-------------
|
|
`pnpm install`
|
 Install all workspace dependencies 
|
|
`pnpm run build`
|
 Build all packages 
|
|
`pnpm run typecheck`
|
 Full TypeScript check across all packages 
|
|
`pnpm --filter @workspace/api-server run dev`
|
 Start backend dev server 
|
|
`pnpm --filter @workspace/parkease run dev`
|
 Start frontend dev server 
|
|
`pnpm --filter @workspace/db run push`
|
 Push DB schema changes 
|
|
`pnpm --filter @workspace/api-spec run codegen`
|
 Regenerate API hooks & Zod schemas 
|
---
## 🌐 API Endpoints
|
 Method 
|
 Route 
|
 Description 
|
|
--------
|
-------
|
-------------
|
|
 GET 
|
`/api/health`
|
 Health check 
|
|
 GET 
|
`/api/spots`
|
 List all spots (with filters) 
|
|
 GET 
|
`/api/spots/:id`
|
 Get spot details 
|
|
 POST 
|
`/api/spots`
|
 Create a new spot 
|
|
 GET 
|
`/api/bookings`
|
 List bookings 
|
|
 POST 
|
`/api/bookings`
|
 Create a booking 
|
|
 PATCH 
|
`/api/bookings/:id`
|
 Update booking status 
|
|
 GET 
|
`/api/users/:id`
|
 Get user profile 
|
|
 GET 
|
`/api/reviews`
|
 Get reviews for a spot 
|
|
 POST 
|
`/api/reviews`
|
 Post a review 
|
|
 GET 
|
`/api/dashboard`
|
 Dashboard stats 
|
---
## 🏙️ Supported Cities
Mumbai · Delhi · Bengaluru · Hyderabad · Pune · Chennai · Gurugram
---
## 📄 License
MIT
