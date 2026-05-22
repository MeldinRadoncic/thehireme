# TheHireMe - Complete Application Flow

## Overview
TheHireMe is a hiring platform with three frontend applications (Client, Worker, Admin) connected to a shared Supabase backend.

## Architecture Diagram
```
┌─────────────────────────────────────────────────────────────┐
│                         TheHireMe Platform                   │
└─────────────────────────────────────────────────────────────┘

┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐
│   CLIENT APP     │  │   WORKER APP     │  │  ADMIN DASHBOARD │
│  (React Native)  │  │  (React Native)  │  │    (Next.js)     │
│     Expo         │  │      Expo        │  │   Tailwind CSS   │
│  Tailwind CSS    │  │   Tailwind CSS   │  └──────────────────┘
└──────────────────┘  └──────────────────┘          │
         │                    │                      │
         └────────────────────┴──────────────────────┘
                              │
                              ▼
                    ┌──────────────────────┐
                    │  SHARED BACKEND      │
                    │  (Supabase)          │
                    ├──────────────────────┤
                    │ - Database           │
                    │ - Edge Functions     │
                    │ - Authentication     │
                    │ - Real-time Updates  │
                    └──────────────────────┘
```

---

## 1. Client Application Flow (thehireme-client)

### User Type: Clients/Customers
- Browse available services/workers
- Post jobs
- Hire workers
- Track ongoing projects
- Rate and review workers

### Flow Steps:
```
1. User Opens App
   ↓
2. Authentication
   - Login/Register via Backend
   - Session management
   ↓
3. Browse Dashboard
   - View available workers
   - View job recommendations
   ↓
4. Post a Job
   - Fill job details
   - Submit to Backend
   ↓
5. Receive Proposals
   - Get worker proposals
   - Review worker profiles
   ↓
6. Hire Worker
   - Accept proposal
   - Start project
   ↓
7. Communication
   - Chat with worker (via Backend)
   - Share updates
   ↓
8. Complete Project
   - Rate worker
   - Leave review
```

---

## 2. Worker Application Flow (thehireme-worker)

### User Type: Service Providers/Workers
- Browse available jobs
- Submit proposals
- Manage projects
- Track earnings
- Build portfolio

### Flow Steps:
```
1. User Opens App
   ↓
2. Authentication
   - Login/Register via Backend
   - Profile setup
   ↓
3. Browse Jobs
   - View job listings
   - Filter by category/price
   ↓
4. Submit Proposal
   - Write proposal message
   - Set bid price
   - Submit to Backend
   ↓
5. Get Hired
   - Receive notification
   - Project starts
   ↓
6. Work on Project
   - View project details
   - Upload work samples
   - Communicate with client
   ↓
7. Complete Project
   - Submit final work
   - Get paid
   - Receive rating
```

---

## 3. Admin Dashboard Flow (thehireme-admin)

### User Type: Platform Administrators
- Monitor platform activity
- Manage users
- Review disputes
- View analytics
- Manage payments

### Flow Steps:
```
1. Admin Logs In
   ↓
2. Dashboard Overview
   - View key metrics
   - Monitor active projects
   - Check user stats
   ↓
3. User Management
   - View all users
   - Manage user accounts
   - Handle complaints
   ↓
4. Payment Management
   - Monitor transactions
   - Handle disputes
   - Process payments
   ↓
5. Content Moderation
   - Review job postings
   - Check user profiles
   - Approve/reject content
   ↓
6. Analytics & Reporting
   - View platform metrics
   - Generate reports
   - Track growth
```

---

## 4. Backend Services (thehireme-backend)

### Database Schema
```
Tables:
├── users
│   ├── id (UUID)
│   ├── email
│   ├── user_type (client/worker)
│   └── timestamps
├── jobs
│   ├── id
│   ├── client_id (FK users)
│   ├── title
│   ├── description
│   └── status
├── proposals
│   ├── id
│   ├── job_id (FK jobs)
│   ├── worker_id (FK users)
│   ├── price_bid
│   └── status
├── projects
│   ├── id
│   ├── job_id (FK jobs)
│   ├── worker_id (FK users)
│   └── status
└── payments
    ├── id
    ├── project_id (FK projects)
    ├── amount
    └── status
```

### Edge Functions
- `hello` - Sample function (can be expanded)
- Custom RPC functions for business logic

### Migrations
- Initial schema setup (20240101000000_init.sql)
- Define tables, indexes, constraints

### Database Seeding
- Sample users (clients and workers)
- Test data for development

---

## 5. Data Flow Between Applications

### Client → Backend
```
Client App
    ↓
1. User logs in
2. Fetches job recommendations
3. Posts a new job
4. Views proposals
5. Accepts proposal
6. Communicates with worker
    ↓
Backend (Supabase)
    ↓
- Stores user session
- Queries jobs table
- Inserts job record
- Queries proposals table
- Updates project status
- Stores messages
```

### Worker → Backend
```
Worker App
    ↓
1. User logs in
2. Fetches available jobs
3. Submits proposal
4. Gets hired
5. Uploads work
6. Completes project
    ↓
Backend (Supabase)
    ↓
- Stores user session
- Queries jobs table
- Inserts proposal record
- Updates project status
- Stores work files
- Updates payment status
```

### Admin → Backend
```
Admin Dashboard
    ↓
1. Views user list
2. Reviews transactions
3. Moderates content
4. Generates reports
    ↓
Backend (Supabase)
    ↓
- Queries all users
- Aggregates payment data
- Queries content for review
- Generates analytics
```

---

## 6. Authentication & Security

### Flow:
```
User Registration/Login
    ↓
Send credentials to Backend
    ↓
Backend validates & stores session
    ↓
Return session token
    ↓
App stores token locally
    ↓
Include token in future requests
    ↓
Backend validates token on each request
```

### Protected Resources:
- User profiles (only own profile accessible)
- Job details (visible to relevant parties only)
- Messages (only visible to participants)
- Payments (admin only)

---

## 7. Real-time Features

### Notifications:
- Job posted → Workers get notifications
- Proposal submitted → Client gets notification
- Project started → Both parties notified
- Message sent → Real-time chat

### Implementation:
- Supabase Realtime subscriptions
- Push notifications to mobile apps
- Email notifications for key events

---

## 8. Payment & Transactions

### Flow:
```
Client posts job → Worker submits proposal → Client accepts proposal
    ↓
Project starts
    ↓
Worker completes work
    ↓
Client approves work
    ↓
Payment initiated
    ↓
Backend processes payment
    ↓
Worker receives payment
    ↓
Transaction recorded in database
```

---

## 9. Deployment Strategy

### Each Application Deployed Independently:
- **Client App**: Deploy to App Store / Google Play (via Expo)
- **Worker App**: Deploy to App Store / Google Play (via Expo)
- **Admin Dashboard**: Deploy to Vercel (Next.js)
- **Backend**: Deploy to Supabase (Hosted Platform)

### Environment Variables:
- Backend URL for all frontend apps
- API keys for third-party services
- Authentication secrets

---

## 10. Development Workflow

### Local Development:
```bash
# Terminal 1: Backend
cd backend
npm run dev

# Terminal 2: Client
cd client
npm run web

# Terminal 3: Worker
cd worker
npm run web

# Terminal 4: Admin
cd admin-dashboard
npm run dev
```

### Git Workflow:
- Each project has its own repository
- Independent versioning and deployments
- Shared documentation in main repo

---

## 11. Future Enhancements

- [ ] Video call integration
- [ ] Escrow payment system
- [ ] Advanced rating algorithm
- [ ] Mobile push notifications
- [ ] Dark mode support
- [ ] Internationalization (i18n)
- [ ] Two-factor authentication
- [ ] Dispute resolution system

---

## 12. Troubleshooting Guide

### Common Issues:

**Issue**: Client can't connect to backend
- **Solution**: Check backend URL in env variables, ensure Supabase is running

**Issue**: Authentication fails
- **Solution**: Clear app cache, verify session token, check backend logs

**Issue**: Data not syncing in real-time
- **Solution**: Check Supabase realtime subscriptions, verify permissions

---

## Contact & Support

For questions about this architecture, refer to individual project README files or CLAUDE.md in each repository.
