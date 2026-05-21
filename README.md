# TheHireMe

A comprehensive hiring platform with separate client, worker, admin, and backend repositories.

## Repositories

| Project | Repo | Tech Stack |
|---------|------|-----------|
| Client App | [thehireme-client](https://github.com/MeldinRadoncic/thehireme-client) | React Native, Expo, Tailwind CSS |
| Worker App | [thehireme-worker](https://github.com/MeldinRadoncic/thehireme-worker) | React Native, Expo, Tailwind CSS |
| Admin Dashboard | [thehireme-admin](https://github.com/MeldinRadoncic/thehireme-admin) | Next.js, Tailwind CSS |
| Backend | [thehireme-backend](https://github.com/MeldinRadoncic/thehireme-backend) | Supabase, PostgreSQL, Edge Functions |

## Quick Start

Clone this repository and navigate to the desired project:

```bash
# Client App
cd client
npm install
npm run web

# Worker App
cd worker
npm install
npm run web

# Admin Dashboard
cd admin-dashboard
npm install
npm run dev

# Backend
cd backend
npm install
npm run dev
```

## Architecture

The platform follows a microservices architecture with:
- **Frontend Applications**: Three separate React Native and Next.js applications
- **Shared Backend**: Single Supabase backend serving all frontend applications
- **Independent Repositories**: Each project can be deployed independently

## Development

Each project is a separate repository and can be developed, tested, and deployed independently while sharing the same backend infrastructure.
