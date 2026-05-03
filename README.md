# 🚀 Backend API — Node.js + Fastify

A RESTful API built with **Fastify** and **MySQL**, featuring **JWT authentication**, user registration, login, and protected user data access.

---

## 🛠️ Technologies

- ⚡ Node.js  
- 🚀 Fastify  
- 🗄️ MySQL (@fastify/mysql)  
- 🔐 JWT (@fastify/jwt)  
- 🔒 Bcrypt  
- 🌍 CORS (@fastify/cors)  
- ⚙️ dotenv  
- ✅ Zod (validation)

---

## 📁 Project Structure

```
├── app.js        # Server setup, plugins and DB connection
├── login.js      # Authentication routes (login, register, me)
├── .env          # Environment variables (not committed)
└── package.json
```

---

## ⚙️ Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/AshleyGotora/backend-nodejs.git
cd backend-nodejs
```

### 2. Install dependencies

```bash
npm install
```

### 3. Create the `.env` file

```env
PORT=3000
DB_HOST=localhost
DB_USER=your_mysql_user
DB_PASS=your_mysql_password
DB_NAME=your_database_name
JWT_SECRET=your_secret_key
```

### 4. Set up the database

Run the following SQL to create the required tables:

```sql
CREATE TABLE login (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(20),
  surname VARCHAR(20),
  email VARCHAR(60) UNIQUE,
  password VARCHAR(255),
  created_on TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);
```

### 5. Run the server

```bash
node app.js
```

Server will be running at: `http://localhost:3000`

---

## 📡 API Routes

| Method | Route | Description | Auth Required |
|--------|-------|-------------|---------------|
| POST | `/login` | Login with email and password | ❌ |
| POST | `/signin` | Register a new user | ❌ |
| GET | `/me` | Get logged-in user data | ✅ |

---

## 🔐 Authentication

This API uses **JWT (JSON Web Token)** for authentication.

After a successful login, you receive a token:

```json
{
  "message": "Login successful",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
}
```

Use this token in the `Authorization` header for protected routes:

```
Authorization: Bearer <your_token>
```

---

## 📝 Request Examples

### Register a user

### Signin

```json
POST /signin
{
  "name": "Ashley",
  "surname": "Gotora",
  "email": "ashley@email.com",
  "password": "123456"
}
```

### Login

```json
POST /login
{
  "email": "ashley@email.com",
  "password": "123456"
}
```

### Get current user

```http
GET /me
Authorization: Bearer <token>
```

Response:

```json
{
  "id": 1,
  "name": "Ashley",
  "surname": "Gotora",
  "email": "ashley@email.com"
}
```

---

## 🔒 Security Notes

- Passwords are hashed using bcrypt
- SQL queries use parameter binding (prevents SQL injection)
- JWT tokens expire after 1 day
- Input validation is handled with Zod
- JWT is required for protected routes (`/me`)

---

## 🚀 Future Improvements

- Rate limiting (anti brute-force protection)
- Refresh tokens
- Role-based access (admin/user)
- Better error handling standardization
- Clean architecture (controllers/services separation)

---

## 👤 Author

**Ashley Gotora**  
[GitHub](https://github.com/AshleyGotora)

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
