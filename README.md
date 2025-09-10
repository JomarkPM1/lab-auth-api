# Lab Auth API

A simple authentication API built with **Node.js**, **Express**, and **MySQL**.  
This project provides user signup, login, token-based authentication using JWT, and protected routes such as fetching the user profile.  

---

## 🚀 Project Overview
The API allows users to:
- Create an account (`/auth/signup`)
- Log in and receive a JWT token (`/auth/login`)
- Access a protected profile endpoint (`/profile`)
- Manage token revocation for logout

The backend is connected to a MySQL database and uses token validation for secure access.

---

## ⚙️ Setup Instructions

### 1. Clone the repository
```bash
git clone https://github.com/your-username/lab-auth-api.git
cd lab-auth-api
````

### 2. Install dependencies

```bash
npm install
```

### 3. Setup the database

Open MySQL and create the database and tables:

```sql
CREATE DATABASE lab_auth;
USE lab_auth;

CREATE TABLE IF NOT EXISTS users (
  id INT AUTO_INCREMENT PRIMARY KEY,
  email VARCHAR(100) NOT NULL UNIQUE,
  password_hash VARCHAR(255) NOT NULL,
  full_name VARCHAR(120),
  role VARCHAR(30) DEFAULT 'student',
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
) ENGINE=INNODB DEFAULT CHARSET=utf8mb4;

CREATE TABLE IF NOT EXISTS revoked_tokens (
  id INT AUTO_INCREMENT PRIMARY KEY,
  jti VARCHAR(64) NOT NULL UNIQUE,
  expires_at DATETIME NOT NULL,
  revoked_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
) ENGINE=INNODB DEFAULT CHARSET=utf8mb4;
```

### 4. Configure environment variables

Create a `.env` file in the project root:

```env
SERVER_PORT=3000
DB_HOST=localhost
DB_USER=root
DB_PASSWORD=yourpassword
DB_NAME=lab_auth
JWT_SECRET=supersecretkey
```

### 5. Run the server

```bash
npm run dev
```

The server will run at:
👉 `http://localhost:3000`

---

## 📡 API Endpoints

### 🔑 Auth

#### Signup

**POST** `/api/auth/signup`
Create a new user account.
**Body (JSON):**

```json
{
  "email": "test@example.com",
  "password": "password123",
  "full_name": "John Doe"
}
```

#### Login

**POST** `/api/auth/login`
Log in and receive a JWT token.
**Body (JSON):**

```json
{
  "email": "test@example.com",
  "password": "password123"
}
```

---

### 👤 Profile

**GET** `/api/profile`
Access protected user profile.
**Headers:**

```
Authorization: Bearer <token>
```

---

### ❤️ Health Check

**GET** `/api/health`
Returns server and DB connection status.

