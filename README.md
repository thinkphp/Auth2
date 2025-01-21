# Authentication System with Welcome Page

A simple authentication system built with React and Node.js, featuring user registration, login, and a welcome page.

## Features

- User registration with username and email
- User login with email and password
- Protected welcome page
- Session management using localStorage
- Responsive design using Tailwind CSS

## Tech Stack

### Frontend
- React
- React Router DOM
- Tailwind CSS

### Backend
- Node.js
- Express.js
- SQLite3
- bcrypt

## Setup Instructions

### Backend Setup

1. Create project directory:
```bash
mkdir auth-system
cd auth-system
mkdir server
cd server
```

2. Initialize Node.js project:
```bash
npm init -y
```

3. Install dependencies:
```bash
npm install express sqlite3 bcrypt cors
```

4. Create server.js and add the following code:
```javascript
const express = require('express');
const sqlite3 = require('sqlite3').verbose();
const bcrypt = require('bcrypt');
const cors = require('cors');

const app = express();
app.use(express.json());
app.use(cors());

// Database setup
const db = new sqlite3.Database('users.db');

// Create users table
db.run(`
    CREATE TABLE IF NOT EXISTS users (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        username TEXT UNIQUE NOT NULL,
        email TEXT UNIQUE NOT NULL,
        password TEXT NOT NULL,
        created_at DATETIME DEFAULT CURRENT_TIMESTAMP
    )
`);

// Routes for register and login
// ... (copy from server code)

app.listen(5000, () => console.log('Server running on port 5000'));
```

### Frontend Setup

1. Create React project:
```bash
cd ..
npm create vite@latest client -- --template react
cd client
```

2. Install dependencies:
```bash
npm install react-router-dom
npm install -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

3. Configure Tailwind CSS in `tailwind.config.js`:
```javascript
/** @type {import('tailwindcss').Config} */
export default {
  content: [
    "./index.html",
    "./src/**/*.{js,ts,jsx,tsx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}
```

4. Add to `src/index.css`:
```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

## Project Structure

```
auth-system/
├── server/
│   ├── server.js
│   ├── package.json
│   └── users.db
└── client/
    ├── src/
    │   ├── components/
    │   │   ├── Auth.jsx
    │   │   └── WelcomePage.jsx
    │   ├── App.jsx
    │   └── index.css
    └── package.json
```

## Running the Application

1. Start the backend:
```bash
cd server
node server.js
```

2. Start the frontend (in a new terminal):
```bash
cd client
npm run dev
```

## API Endpoints

### Register User
```bash
POST http://localhost:5000/api/register
Content-Type: application/json

{
    "username": "john_doe",
    "email": "john@example.com",
    "password": "password123"
}
```

### Login User
```bash
POST http://localhost:5000/api/login
Content-Type: application/json

{
    "email": "john@example.com",
    "password": "password123"
}
```

## Database Management

View database contents:
```bash
sqlite3 users.db
.tables
SELECT * FROM users;
```

## Local Storage

The application stores user session data in localStorage:
- Key: `'user'`
- Value: `{ id, username, email }`

## Security Features

- Password hashing using bcrypt
- Protected routes in frontend
- Form validation
- Error handling for duplicate email/username

## Common Issues

1. Server Connection Error
   - Ensure server is running on port 5000
   - Check CORS configuration

2. Database Issues
   - Verify SQLite3 is installed
   - Check file permissions for users.db

3. Login Issues
   - Clear localStorage and try again
   - Verify email and password combination

## Future Improvements

- Add JWT authentication
- Implement password reset
- Add email verification
- Enhanced error handling
- Add user profile management

## License

MIT License


This README focuses solely on the authentication system and includes:
1. Clear setup instructions
2. Essential features
3. API documentation
4. Database setup
5. Common troubleshooting steps
