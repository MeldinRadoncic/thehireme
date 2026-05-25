# TheHireMe - Main Project

**GitHub Repository:** https://github.com/MeldinRadoncic/thehireme

> ⚠️ **Note:** This is just the central hub that holds the four projects. Each project has its own separate GitHub repository and can be developed independently.

---

## The Hire Me — Solution and Overview

### What is The Hire Me

The Hire Me is a two-sided marketplace platform connecting skilled local service workers with clients across multiple European countries. Workers showcase their services, experience, portfolio through videos and images. Clients discover workers, view their work, and connect directly for inquiries.

### Project Structure

The Hire Me consists of four interconnected projects: worker app, client app, admin dashboard, and backend. All four projects rely on the same Supabase database, Clerk authentication, and Stripe payment system. The worker app and client app are separate React Native mobile apps, while the admin dashboard is a web application. The backend handles business logic, data validation, payment processing, and error logging using Supabase edge functions.

Each project has its own folder, Claude.md file, and docs folder, along with a separate GitHub repository. Each project is independent but connected through the shared backend services.

### Getting Started with Development

Read this main Claude.md first. Then, navigate to the specific project folder (worker, client, admin, or backend). Read that project's Claude.md file and all related docs before writing any code.

### Documentation

The main docs folder contains overall project documentation. Each project folder has its own docs folder with technical guidance specific to that project.

### Development Environment

Use Docker to run a local Supabase instance. All projects connect to the same local Supabase during development.

### Security

Never hardcode API keys or secrets—store all sensitive data in Supabase dashboard environment variables. No sensitive data in URLs. Use parameterized queries, validate all input on the server.

### Performance

Implement rate limiting, pagination, and caching to minimize API costs.

### GitHub Workflow

Each project has its own GitHub repo. Do not push or commit without explicit instructions.

### Supabase MCP

Supabase MCP is already installed in the project. It can be used to inspect production data, ensuring you have full visibility.

### Deployment and Edge Functions

When deploying edge functions or performing database migrations, use the Supabase CLI. Check the Supabase docs for instructions. First, work locally—once everything is verified, deploy using the CLI for migrations and edge functions.

### Permission to Research

If anything is unclear during development—frameworks, implementations, or technical specifics—Claude Code has full permission to go online, consult official docs, and find the best solution. The goal is to never stall—always seek out official guidance if something is confusing.

---

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