# 📊 Financial Records Backend

A clean, structured backend for a **Finance Dashboard System** that supports user roles, financial record management, and analytics.

This project focuses on **real-world backend practices** such as role-based access control, modular architecture, validation, and efficient data querying.

---

# 🚀 Key Features

## 🔐 Authentication & Authorization

* User registration and login
* JWT-based authentication
* Secure cookie handling
* Role-based access control (RBAC)

---

## 👥 User & Role Management

Manage system users with clear access control.

**Capabilities:**

* Create users (Admin)
* Assign roles: `viewer`, `analyst`, `admin`
* Update user details
* Activate / deactivate users
* Delete users

**Role Permissions:**

| Role    | Access              |
| ------- | ------------------- |
| Viewer  | Dashboard only      |
| Analyst | Dashboard + Records |
| Admin   | Full system access  |

---

## 💰 Financial Records Management

Handles all financial transactions efficiently.

**Operations:**

* Create records
* Fetch records with filters
* Update records
* Soft delete records

**Record Fields:**

* Amount
* Type (income / expense)
* Category
* Date
* Notes
* Status (active / deleted)

---

## 🔍 Advanced Querying

Designed for real-world usability:

* Pagination support
* Filtering by type, category, status
* Search using partial matching (`LIKE` queries)

---

## 📈 Dashboard & Analytics APIs

Provides aggregated insights:

* Total Income
* Total Expense
* Net Balance
* Category-wise summary
* Recent transactions
* Trends:

  * Daily
  * Weekly
  * Monthly
  * Yearly
  * Custom date range

---

## 🛡️ Security & Reliability

* Password hashing using bcrypt
* JWT authentication
* HTTP-only cookies
* Helmet for secure headers
* Rate limiting
* Input validation
* Centralized error handling

---

## 🧠 Access Control Matrix

| Action         | Viewer | Analyst | Admin |
| -------------- | ------ | ------- | ----- |
| View Dashboard | ✅      | ✅       | ✅     |
| View Records   | ❌      | ✅       | ✅     |
| Create Record  | ❌      | ❌       | ✅     |
| Update Record  | ❌      | ❌       | ✅     |
| Delete Record  | ❌      | ❌       | ✅     |
| Manage Users   | ❌      | ❌       | ✅     |

---

# 🏗️ Project Structure

```
financial-records-backend/
├── database/
│   └── finance_dashboard (3).sql
|   └── finance_dashboard.sql
|
├── seeders/
│   └── seedAdmin.js
│
├── src/
│   ├── config/
│   │   └── db.js
│   │
│   ├── controllers/
│   ├── middlewares/
│   ├── models/
│   ├── routes/
│   ├── utils/
│   ├── validators/
│   │
│   └── server.js
│
├── .env
├── package.json
└── README.md
```

---

# 🗄️ Database Design

## Users Table

| Field    | Type    |
| -------- | ------- |
| id       | INT     |
| email    | VARCHAR |
| password | VARCHAR |
| role     | ENUM    |
| status   | ENUM    |

---

## Records Table

| Field    | Type    |
| -------- | ------- |
| id       | INT     |
| amount   | DECIMAL |
| type     | ENUM    |
| category | VARCHAR |
| date     | DATE    |
| notes    | TEXT    |
| status   | ENUM    |

---

## 🧰 Tech Stack

* Backend: Node.js, Express.js
* Database: MySQL (mysql2)
* Authentication: JWT (jsonwebtoken) + HTTP-only cookies
* Security: Helmet, Express Rate Limit, Cookie Parser
* Validation: express-validator
* Password Hashing: bcryptjs
* Architecture: Role-Based Access Control (RBAC)
* Environment Management: dotenv
* 
---

# ⚙️ Setup Guide (Step-by-Step)

## 1. Clone Repository

```
git clone https://github.com/taniya-rastogi/financial-records.git
cd financial-records-backend
```

## 2. Install Dependencies

```
npm install
```

## 3. Configure Environment Variables

Create a `.env` file:

```
PORT=3000

FRONTEND_URL_1=http://127.0.0.1:5500
FRONTEND_URL_2=http://127.0.0.1:5501

JWT_SECRET=your_secret_key
COOKIE_SECURE=false
COOKIE_SAMESITE=lax

DB_HOST=127.0.0.1
DB_USER=root
DB_PASSWORD=
DB_NAME=finance_dashboard

ADMIN_EMAIL=admin@gmail.com
ADMIN_PASSWORD=admin123
```

## 4. Setup Database

* Create database: `finance_dashboard`
* Import provided SQL schema

## 5. Seed Admin User

```
node seeders/seedAdmin.js
```

## 6. Start Server

```
node src/server.js
```

Server will run on:
👉 [http://localhost:3000](http://localhost:3000)

---

# 📡 API Reference

## 🔐 Authentication

| Method | Endpoint           |
| ------ | ------------------ |
| POST   | /api/auth/register |
| POST   | /api/auth/login    |

---

## 👥 Users (Admin Only)

| Method | Endpoint            |
| ------ | ------------------- |
| GET    | /api/users          |
| POST   | /api/users          |
| PUT    | /api/users/:id      |
| PATCH  | /api/users/:id/role |
| DELETE | /api/users/:id      |

---

## 💰 Records

| Method | Endpoint         | Access         |
| ------ | ---------------- | -------------- |
| POST   | /api/records     | Admin          |
| GET    | /api/records     | Analyst, Admin |
| PUT    | /api/records/:id | Admin          |
| DELETE | /api/records/:id | Admin          |

---

## 📊 Dashboard

| Method | Endpoint                     |
| ------ | ---------------------------- |
| GET    | /api/dashboard/summary       |
| GET    | /api/dashboard/category      |
| GET    | /api/dashboard/recent        |
| GET    | /api/dashboard?trend=monthly |

---

# 🔄 Data Handling Decisions

## Soft Delete

* Records are not permanently removed
* Status updated to `deleted`
* Hidden from non-admin users

## Pagination

* Default limit: 5
* Query: `?page=1`

## Search

* Partial matching using SQL `LIKE`
* Applied on type and category

---

# ⚖️ Design Choices

* Relational database (MySQL) for structured data
* Middleware-based RBAC for clean separation
* Cookie-based JWT authentication
* Raw SQL for better control and clarity

---

# 📌 Final Notes

This project demonstrates:

* Scalable backend structure
* Clean separation of concerns
* Secure authentication & authorization
* Efficient data aggregation

Focus is on **clarity, maintainability, and practical backend design**.

---

## 📌 Author

Taniya Rastogi
| Backend-focused developer (Node.js | Express | MySQL)

