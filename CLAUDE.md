# TheHireMe - Main Project

**GitHub Repository:** https://github.com/MeldinRadoncic/thehireme

## Project Overview
TheHireMe is a comprehensive platform with 4 separate repositories:

### 1. Client App (React Native)
- **Repo:** https://github.com/MeldinRadoncic/thehireme-client
- **Purpose:** Client-side application for users
- **Tech:** React Native, Expo, Tailwind CSS

### 2. Worker App (React Native)
- **Repo:** https://github.com/MeldinRadoncic/thehireme-worker
- **Purpose:** Worker/provider application
- **Tech:** React Native, Expo, Tailwind CSS

### 3. Admin Dashboard (Next.js)
- **Repo:** https://github.com/MeldinRadoncic/thehireme-admin
- **Purpose:** Admin panel for platform management
- **Tech:** Next.js, Tailwind CSS

### 4. Backend (Supabase)
- **Repo:** https://github.com/MeldinRadoncic/thehireme-backend
- **Purpose:** Shared backend services, database, edge functions
- **Tech:** Supabase, PostgreSQL, Edge Functions

## Project Structure
```
THEHIREME/
├── client/              # Client app repository
├── worker/              # Worker app repository
├── admin-dashboard/     # Admin dashboard repository
├── backend/             # Backend repository
└── docs/                # Documentation
```

## Getting Started
Each project has its own repository and can be developed independently.

### Client
```bash
cd client
npm install
npm run web
```

### Worker
```bash
cd worker
npm install
npm run web
```

### Admin Dashboard
```bash
cd admin-dashboard
npm install
npm run dev
```

### Backend
```bash
cd backend
npm install
npm run dev
```

## Architecture
All 3 frontend applications (client, worker, admin) consume data and services from the shared backend (thehireme-backend).