# JobTrackr 🚀 — Intelligent Job Application Tracker & Career Pipeline

> **Master of Computer Applications (MCA) Final Year Capstone Project**  
> A production-grade, full-stack MERN web application engineered to streamline the recruitment process. Organize applications, visualize recruitment pipelines on an interactive Kanban board, track interview milestones, monitor conversion rates with MongoDB aggregation analytics, and never miss a follow-up.

---

## 🌟 Key Features

- **Interactive Kanban Pipeline**: Drag-and-drop job application cards across recruitment stages (`Wishlist`, `Applied`, `Interview`, `Offer`, `Rejected`) powered by `@dnd-kit` with instant optimistic updates and automatic server sync.
- **MongoDB Aggregation Analytics**: Real-time statistical dashboard with dynamic Recharts visualizations:
  - 5 key KPI stat cards: Total Tracked, In Interview, Offers Received, Rejections, and Response Rate %.
  - Donut chart displaying the pipeline status distribution.
  - 6-month continuous bar chart tracking application velocity and consistency.
  - Upcoming and overdue recruiter follow-up reminders.
- **Advanced Filtering, Search & Sorting**:
  - Debounced real-time search across company, position, and location.
  - Granular filters by status (`Wishlist`, `Applied`, `Interview`, `Offer`, `Rejected`) and job type (`Full-time`, `Internship`, `Part-time`, `Contract`).
  - Sort by newest applied, oldest applied, company name (A-Z / Z-A), and recently updated.
  - Toggle between responsive **Card Grid View** and **Data Table View**.
  - Server-side pagination (10 items per page) with page navigation controls.
- **Robust Security & User Authentication**:
  - JWT (JSON Web Token) with 7-day expiration in HTTP `Authorization: Bearer` headers.
  - Passwords securely hashed with `bcryptjs` (salt factor 10, excluded from query results by default).
  - Rate limiting on authentication endpoints to prevent brute-force attacks.
  - HTTP security headers with `helmet` and strict `cors` origin whitelisting.
  - Comprehensive input validation using `express-validator` with clean, field-specific error feedback.
  - Axios request/response interceptors with automatic session restore (`/api/auth/me`) and graceful 401 handling.
- **Modern, Accessible UI/UX**:
  - Designed with Tailwind CSS with custom branding colors.
  - Persistent Dark / Light mode toggle synchronized with `localStorage` and OS preferences.
  - Responsive mobile drawer navigation with touch support.
  - Loading skeletons, empty states, confirmation dialogs, and interactive `react-hot-toast` notifications.
- **Zero-Config Evaluation Seed Script**:
  - Preloaded with a realistic demo profile (`demo@jobtrackr.com` / `Demo@1234`) and 25 realistic sample applications spread across different stages, companies (Google, Microsoft, Stripe, Amazon, etc.), and past 6 months.

---

## 🛠️ Technology Stack

| Layer | Technologies |
|---|---|
| **Frontend** | React 18, Vite, React Router v6, Tailwind CSS, Axios, Lucide React, Recharts, @dnd-kit/core, React Hot Toast |
| **Backend** | Node.js (v20+), Express.js, MongoDB, Mongoose ODM, JSON Web Tokens (jsonwebtoken), bcryptjs, express-validator |
| **Security & Middleware** | Helmet, CORS, Express Rate Limit, Morgan, Dotenv |
| **Testing & Tools** | MongoMemoryServer (standalone execution fallback), Chrome DevTools |

---

## 📂 Project Directory Structure

```text
jobtrackr/
├── package.json               # Root scripts to orchestrate client and server
├── .gitignore                 # Ignore node_modules, build outputs, and .env
├── README.md                  # Comprehensive project documentation
├── screenshots/               # High-resolution screenshots of the UI
├── server/                    # Node.js + Express Backend
│   ├── package.json
│   ├── server.js              # Express app entry & HTTP configuration
│   ├── seed.js                # Database seeder (25 sample jobs + demo user)
│   ├── .env.example           # Example environment variables
│   ├── .env                   # Local environment configuration
│   ├── config/
│   │   └── db.js              # Mongoose DB connection & in-memory fallback
│   ├── models/
│   │   ├── User.js            # User schema with bcrypt pre-save hook
│   │   └── Job.js             # Job schema with compound indexes
│   ├── controllers/
│   │   ├── authController.js  # Register, login, me, update profile
│   │   └── jobController.js   # CRUD, status patch, aggregation stats
│   ├── middleware/
│   │   ├── auth.js            # JWT Bearer verification middleware
│   │   ├── errorHandler.js    # Centralized error handler
│   │   └── validate.js        # express-validator result handler
│   └── routes/
│       ├── authRoutes.js      # Auth endpoints with rate limiting
│       └── jobRoutes.js       # Job endpoints scoped to current user
└── client/                    # React 18 + Vite Frontend
    ├── package.json
    ├── vite.config.js         # Vite configuration with API proxy
    ├── tailwind.config.js     # Tailwind CSS theme & dark mode config
    ├── postcss.config.js
    ├── index.html
    └── src/
        ├── main.jsx           # React DOM root entry
        ├── App.jsx            # Application layout, routes & toaster
        ├── index.css          # Tailwind base & custom scrollbar styles
        ├── api/
        │   └── axios.js       # Axios instance with interceptors
        ├── context/
        │   ├── AuthContext.jsx   # Authentication state management
        │   └── ThemeContext.jsx  # Dark/Light theme state
        ├── components/
        │   ├── common/        # Navbar, Footer, Modal, ConfirmDialog, Skeleton
        │   ├── jobs/          # JobCard, JobTable, JobFilterBar, JobModal
        │   └── board/         # KanbanBoard, KanbanColumn, KanbanCard
        └── pages/
            ├── Home.jsx       # Landing page with hero & feature preview
            ├── Login.jsx      # Login page with demo one-click fill
            ├── Register.jsx   # Registration with live password strength
            ├── Dashboard.jsx  # Analytics overview & Recharts graphs
            ├── Jobs.jsx       # Application catalog with pagination
            ├── Board.jsx      # Drag-and-drop Kanban board
            ├── Profile.jsx    # User settings & password change
            └── NotFound.jsx   # Custom 404 page
```

---

## ⚡ Quick Start Guide

### Prerequisites
- [Node.js](https://nodejs.org/) (v18.0.0 or higher)
- [MongoDB](https://www.mongodb.com/) (Local mongod service or a free [MongoDB Atlas](https://www.mongodb.com/atlas) cluster)
  > *Note: If no local MongoDB is detected, the server automatically starts an embedded in-memory MongoDB instance for hassle-free zero-config testing.*

### 1. Clone & Setup Workspace
```bash
cd jobtrackr
```

### 2. Configure Backend Environment
Create `server/.env` (or copy from `server/.env.example`):
```env
PORT=5000
NODE_ENV=development
MONGODB_URI=mongodb://localhost:27017/jobtrackr
JWT_SECRET=jobtrackr_super_secret_jwt_key_2026_mca_final_project
JWT_EXPIRES_IN=7d
CLIENT_URL=http://localhost:5173
```

### 3. Install Dependencies
```bash
# Install backend dependencies
cd server
npm install

# Install frontend dependencies
cd ../client
npm install
```

### 4. Seed Demo Data
Populate the database with the preconfigured demo account and 25 realistic sample jobs:
```bash
cd server
npm run seed
```

**Demo Account Credentials:**
- **Email**: `demo@jobtrackr.com`
- **Password**: `Demo@1234`
*(You can also use the one-click "Auto-Fill" button on the login screen).*

### 5. Run the Application
Open two terminal windows:

**Terminal 1 (Backend API Server):**
```bash
cd server
npm run dev
# Server starts at http://localhost:5000
```

**Terminal 2 (Frontend Client):**
```bash
cd client
npm run dev
# Vite dev server starts at http://localhost:5173
```

Navigate to `http://localhost:5173` in your browser.

---

## 📋 REST API Reference

All `/api/jobs` routes and `/api/auth/me` require the `Authorization: Bearer <token>` header.

| Method | Endpoint | Description | Request Body |
|---|---|---|---|
| `POST` | `/api/auth/register` | Register a new user account | `{ name, email, password }` |
| `POST` | `/api/auth/login` | Authenticate user & get 7-day JWT | `{ email, password }` |
| `GET` | `/api/auth/me` | Fetch authenticated user profile & count | *None* |
| `PUT` | `/api/auth/profile` | Update user name and/or password | `{ name, currentPassword, newPassword }` |
| `GET` | `/api/jobs` | Get paginated jobs with search & filter | Query: `?search=&status=&jobType=&sort=&page=&limit=` |
| `POST` | `/api/jobs` | Create a new job tracker application | `{ company, position, location, jobType, status, salary, source, jobLink, appliedDate, followUpDate, notes }` |
| `GET` | `/api/jobs/:id` | Get details of a single job | *None* |
| `PUT` | `/api/jobs/:id` | Update full details of a job | `{ company, position, status, ... }` |
| `PATCH`| `/api/jobs/:id/status`| Update application status (Kanban drop) | `{ status: "Interview" }` |
| `DELETE`| `/api/jobs/:id` | Delete a job application | *None* |
| `GET` | `/api/jobs/stats` | Aggregate dashboard statistics | *None* |
| `GET` | `/api/health` | Health check and uptime ping | *None* |

---

## 🚀 Deployment Guide

### 1. Database: MongoDB Atlas
1. Create a free M0 cluster at [MongoDB Atlas](https://www.mongodb.com/atlas).
2. Create a database user with read/write privileges.
3. Allow network access from anywhere (`0.0.0.0/0`) or your Render server IP.
4. Copy the connection string (e.g., `mongodb+srv://<user>:<password>@cluster0.mongodb.net/jobtrackr?retryWrites=true&w=majority`).

### 2. Backend: Render
1. Create a new **Web Service** on [Render](https://render.com) connected to your GitHub repository.
2. Set **Root Directory** to `server`.
3. Set **Build Command** to `npm install`.
4. Set **Start Command** to `node server.js`.
5. Add Environment Variables:
   - `NODE_ENV`: `production`
   - `PORT`: `10000`
   - `MONGODB_URI`: `<Your MongoDB Atlas Connection String>`
   - `JWT_SECRET`: `<Secure Random 64-character String>`
   - `JWT_EXPIRES_IN`: `7d`
   - `CLIENT_URL`: `https://your-jobtrackr-client.vercel.app`

### 3. Frontend: Vercel
1. Import your repository into [Vercel](https://vercel.com).
2. Set **Root Directory** to `client`.
3. Framework Preset: **Vite**.
4. In `client/vite.config.js` or via environment variable `VITE_API_BASE_URL`, point Axios calls to your live Render backend URL (`https://your-backend.onrender.com/api`).
5. Deploy.

---

## 📷 Screenshots

| View | Screenshot |
|---|---|
| **Landing Page** | `screenshots/01-landing-page.png` |
| **Login with Demo Auto-Fill** | `screenshots/02-login.png` |
| **Registration Form** | `screenshots/03-register.png` |
| **Analytics Dashboard** | `screenshots/04-dashboard.png` |
| **Applications Catalog** | `screenshots/05-jobs-list.png` |
| **Add / Edit Application Modal** | `screenshots/06-add-job-modal.png` |
| **Kanban Pipeline Board** | `screenshots/07-kanban-board.png` |
| **User Profile & Security** | `screenshots/08-profile.png` |
| **Mobile Responsive Layout** | `screenshots/09-mobile-view.png` |

---

## 🎓 Academic Declaration
This project is developed as part of the MCA (Master of Computer Applications) final year curriculum. It demonstrates full-stack software architecture principles, decoupled client-server interaction via RESTful APIs, relational data modeling with non-relational database indexes, user authentication lifecycles, and modern reactive component architectures.
