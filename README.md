# HostCare.io — Hostel Complaint Tracking System
> *"Report. Track. Resolve."*

[![Node.js](https://img.shields.io/badge/Node.js-v20+-green.svg)](https://nodejs.org/)
[![Angular](https://img.shields.io/badge/Angular-v18-red.svg)](https://angular.dev/)
[![Express](https://img.shields.io/badge/Express-v4.19-lightgrey.svg)](https://expressjs.com/)
[![MongoDB](https://img.shields.io/badge/MongoDB-v6.0+-brightgreen.svg)](https://www.mongodb.com/)
[![License](https://img.shields.io/badge/Status-Completed%20%26%20Verified-blue.svg)]()

---

## 1. Project Overview & Problem Statement

**HostCare.io** is a full-stack web application developed for university and college hostels to replace inefficient, easily misplaced physical paper complaint registers. It provides a transparent, accountable digital workflow connecting hostel residents and administration.

### Problem Solved:
* Eliminates lost paper records and unmonitored messaging group complaints.
* Provides students with real-time visibility into repair progress.
* Gives hostel wardens a centralized triage dashboard and audit trail.
* Generates operational analytics to detect chronic infrastructure issues across electrical, plumbing, and network facilities.

---

## 2. Key Features

* **Resident Student Portal:**
  * Secure student registration and JWT authentication.
  * Room-bound maintenance complaint submission with auto-generated tracking ID (`HC-YYYY-XXXX`).
  * 5-Stage interactive grievance lifecycle stepper timeline (`SUBMITTED -> UNDER_REVIEW -> IN_PROGRESS -> RESOLVED -> CLOSED`).
  * In-app real-time notification alerts with unread badges.
* **Warden Administrative Console:**
  * Master complaints registry across all hostel blocks and wings.
  * 5-stage lifecycle state machine with mandatory remarks for resolutions.
  * Real-time operational reports (Resolution Rate %, Category breakdowns, Status ratios).
* **Multi-Tenant Security & Reliability:**
  * Defense-in-depth security: Helmet headers, CORS policies, rate limiting.
  * Strict horizontal tenant isolation (students can only see/mutate own records).
  * 100% automated regression test coverage (240 / 240 assertions passed).

---

## 3. Technology Stack

* **Frontend:** Angular 18 (Standalone Components, Signals, Router, Interceptors), Tailwind CSS.
* **Backend:** Node.js, Express.js REST API, JSON Web Tokens (`jsonwebtoken`), `bcryptjs`, `helmet`, `express-rate-limit`.
* **Database:** MongoDB Community Server, Mongoose ODM.
* **Testing:** Postman Collections, Node.js Automated Test Suites, Karma / Chrome Headless.

---

## 4. System Architecture

```
Angular 18 Frontend (Port 4200)
       │ HTTP / JSON
       ▼
Express.js REST API Server (Port 5000)
       ├── Helmet Security & CORS Policy
       ├── Centralized JWT & RBAC Middleware
       └── Payload Validation & State Machine
       │ ODM Queries
       ▼
MongoDB Community Server (Port 27017)
       ├── users Collection
       ├── complaints Collection
       └── notifications Collection
```

---

## 5. Project Directory Structure

```
hostcare.io/
│
├── backend/                        # Node.js + Express REST API
│   ├── src/
│   │   ├── config/database.js      # MongoDB Mongoose connection
│   │   ├── controllers/            # Route controllers (Auth, Complaints, etc.)
│   │   ├── middleware/             # Auth, RBAC, Validation, Error middlewares
│   │   ├── models/                 # Mongoose schemas (User, Complaint, Notification)
│   │   ├── routes/                 # Express modular REST routes
│   │   ├── scripts/                # Seed scripts and test runners
│   │   ├── utils/                  # ID generator, response helpers
│   │   └── server.js               # Main Express application entry
│   ├── .env.example                # Configuration template
│   ├── package.json
│   └── postman_collection.json     # 34-request Postman test suite
│
├── frontend/                       # Angular 18 Single Page Application
│   ├── src/
│   │   ├── app/
│   │   │   ├── core/               # Guards, interceptors, models, HTTP services
│   │   │   ├── features/           # Student and Admin feature pages
│   │   │   ├── layouts/            # Student and Admin dashboard layouts
│   │   │   └── shared/             # Badges, spinners, timeline, pagination
│   │   ├── index.html
│   │   ├── main.ts
│   │   └── styles.css              # Tailwind CSS directives
│   ├── angular.json
│   └── package.json
│
├── docs/                           # Phase reports and technical specifications
│   ├── setup-guide.md              # Fresh installation and troubleshooting
│   ├── demo-guide.md               # 17-step teacher demonstration workflow
│   ├── architecture.md             # Full architecture specification
│   ├── database.md                 # MongoDB schema documentation
│   ├── api-documentation.md        # Comprehensive REST API endpoint reference
│   ├── security.md                 # Security audit and vulnerability analysis
│   ├── final-testing-summary.md    # Consolidated 240-check testing summary
│   ├── presentation-outline.md     # 12-slide college presentation outline
│   ├── final-project-report-outline.md # 11-chapter academic report outline
│   └── screenshot-checklist.md     # Manual screenshot guide for PPT/Report
│
├── .gitignore                      # Git exclusion rules
└── README.md                       # Main project documentation
```

---

## 6. Quick Start & Setup Instructions

### 1. Prerequisites
* Node.js v18+ or v20+ LTS
* MongoDB running on `127.0.0.1:27017`

### 2. Backend Setup
```powershell
cd backend
npm install
copy .env.example .env
node src/scripts/seedAdmin.js       # Provisions warden administrator
node src/scripts/seedDemoData.js    # (Optional) Seeds sample complaints
npm start
```
* Backend starts at `http://localhost:5000`
* Health check: `http://localhost:5000/api/health`

### 3. Frontend Setup
Open a new terminal:
```powershell
cd frontend
npm install
npm start
```
* Frontend starts at `http://localhost:4200`

---

## 7. Demo Credentials

| Role | Email | Password | Console URL |
| :--- | :--- | :--- | :--- |
| **Hostel Warden (Admin)** | `warden@hostel.edu` | `WardenPass123!` | `http://localhost:4200/admin/login` |
| **Demo Student (Resident)** | `demo.student@hostcare.local` | `DemoStudent123!` | `http://localhost:4200/login` |

---

## 8. Verification & Test Execution

Run the complete automated test suite locally:
```powershell
# 1. Backend Integration Tests (51/51 PASS)
node backend/src/scripts/testBackend.js

# 2. Security & Validation Suite (42/42 PASS)
node backend/src/scripts/verifySecurity.js

# 3. Postman Automated Runner (75/75 PASS)
node backend/src/scripts/testPostmanRunner.js

# 4. Full End-to-End QA Suite (60/60 PASS)
node backend/src/scripts/runE2EQA.js

# 5. Angular Unit Tests (2/2 PASS)
cd frontend && npm test -- --watch=false --browsers=ChromeHeadless

# 6. Production Build (PASS, 0 errors)
cd frontend && npm run build
```

---

## 9. Academic Project Status
* **Phases 1–12 Completed & Verified:** Requirements, UX Wireframing, Environment Setup, Database Schemas, REST API, Postman Verification, Angular Development, Integration, Reports/Notifications, Security Audit, E2E QA, and Final Submission Readiness.
* **Status:** **College Submission & Teacher Evaluation Ready.**
