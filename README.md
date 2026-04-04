📊 Financial Records Backend

A backend system for a Finance Dashboard Application that manages users, roles, financial records, and provides analytical insights via dashboard APIs.

This project demonstrates clean backend architecture, role-based access control, data modeling, validation, and aggregation logic.

🚀 Features
🔐 1. Authentication & Authorization
User registration & login
JWT-based authentication
Cookie-based session handling
Role-based access control (RBAC)
👥 2. User & Role Management

Supports:

Create users (Admin)
Assign roles (viewer, analyst, admin)
Update user details
Activate / deactivate users
Delete users

Roles:

Role	Permissions
Viewer	View dashboard only
Analyst	View records + dashboard insights
Admin	Full access (CRUD users & records)
💰 3. Financial Records Management

Supports:

Create records
View records (with filters)
Update records
Soft delete records

Fields:

Amount
Type (income / expense)
Category
Date
Notes
Status (active, deleted)
🔍 4. Advanced Query Features
Pagination
Filtering:
Type
Category
Status (admin only)
Search (partial match on type & category)
📈 5. Dashboard APIs

Provides aggregated data:

Total Income
Total Expense
Net Balance
Category-wise totals
Recent records
Trends:
Daily
Weekly
Monthly
Yearly
Custom date range
🛡️ 6. Security & Best Practices
Password hashing (bcrypt)
JWT authentication
HTTP-only cookies
Helmet (security headers)
Rate limiting
Input validation (express-validator)
Centralized error handling

🧠 7. Access Control Logic
Action	Viewer	Analyst	Admin
View Dashboard	✅	✅	✅
View Records  	❌	✅	✅
Create Record  	❌	❌	✅
Update Record  	❌	❌	✅
Delete Record  	❌	❌	✅
Manage Users  	❌	❌	✅

financial-records-backend/
├── database/
├── seeders/
│   └── seedAdmin.js
│
├── src/
│   ├── config/
│   │   └── db.js
│   │
│   ├── controllers/
│   │   ├── auth.controller.js
│   │   ├── user.controller.js
│   │   ├── record.controller.js
│   │   └── dashboard.controller.js
│   │
│   ├── middlewares/
│   │   ├── auth.middleware.js
│   │   ├── role.middleware.js
│   │   ├── error.middleware.js
│   │   └── validation.middleware.js
│   │
│   ├── models/
│   │   ├── user.model.js
│   │   └── record.model.js
│   │
│   ├── routes/
│   │   ├── auth.routes.js
│   │   ├── user.routes.js
│   │   ├── record.routes.js
│   │   └── dashboard.routes.js
│   │
│   ├── utils/
│   │   └── AppError.js
│   │
│   ├── validators/
│   │   ├── auth.validator.js
│   │   ├── user.validator.js
│   │   └── record.validator.js
│   │
│   └── server.js
│
├── .env
├── package.json
└── README.md

🗄️ Database Design
'users Table'
Field    	    Type
id	          INT
email    	    VARCHAR
password	    VARCHAR
role    	    ENUM
status  	    ENUM
created_at	  TIMESTAMP
updated_at	  TIMESTAMP

'records Table'
Field	        Type
id	          INT
amount		    DECIMAL
type	       	ENUM
category	   	VARCHAR
date	       	DATE
notes		      TEXT
status	     	ENUM
created_at  	TIMESTAMP
updated_at  	TIMESTAMP


⚙️ Setup Instructions

1. Clone Repository
git clone <repo-url>
cd financial-records-backend

2. Install Dependencies
npm install

3. Configure Environment Variables

Create .env file:
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

4. Setup Database
Import SQL schema using phpMyAdmin or MySQL CLI

5. Seed Admin User
node seeders/seedAdmin.js

6. Start Server
node src/server.js

📡 API Endpoints

🔐 Auth

Method	Endpoint
POST	/api/auth/register
POST	/api/auth/login

👥 Users (Admin Only)

Method	Endpoint
GET	/api/users
POST	/api/users
PUT	/api/users/:id
PATCH	/api/users/:id/role
DELETE	/api/users/:id

💰 Records

Method	Endpoint	Access
POST	/api/records	Admin
GET	/api/records	Analyst, Admin
PUT	/api/records/:id	Admin
DELETE	/api/records/:id	Admin

📊 Dashboard

Method	Endpoint
GET	/api/dashboard/summary
GET	/api/dashboard/category
GET	/api/dashboard/recent
GET	/api/dashboard?trend=monthly

🧾 Validation & Error Handling

Centralized error handling using custom AppError
Request validation via express-validator
Proper HTTP status codes:
400 → Bad Request
401 → Unauthorized
403 → Forbidden
404 → Not Found
500 → Server Error

🔄 Data Handling Decisions

Soft Delete
Records are not permanently deleted
Status updated to deleted
Non-admin users cannot see deleted records

Pagination
Default: 5 records per page
Query param: ?page=1

Search
Partial matching using SQL LIKE
Works on:
type
category

⚖️ Design Decisions & Tradeoffs

Used MySQL (Relational DB) for structured financial data
Implemented RBAC via middleware for clean separation
Chose cookie-based JWT for better frontend integration
Used manual SQL queries instead of ORM for simplicity and control
