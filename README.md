# StudCrud — Student Information System

A full-stack student information system with a React interface, Express API, and MySQL/MariaDB database (managed with XAMPP/phpMyAdmin).

## Features

- Admin login and student login
- Students can register their own accounts
- Admin can create, view, update, and delete student records
- Students can view and update only their own profile
- Students cannot change their LRN or ID number; administrators manage those identifiers
- Passwords are hashed with bcrypt
- JWT-based sessions and role-based API authorization
- Responsive dark navy / blue interface

## Requirements

- Node.js 20 or newer
- npm
- XAMPP with MySQL/MariaDB running

## Run locally

1. Open a terminal in the `StudCrud` folder.
2. Install the root development dependency and both app dependencies:

   ```bash
   npm install
   npm run install:all
   ```

3. Create the server environment file:

   ```bash
   cp server/.env.example server/.env
   ```

   Set `JWT_SECRET` to a long, random secret and choose a strong `ADMIN_PASSWORD`. Set `DB_USER`, `DB_PASSWORD`, and `DB_NAME` to match your XAMPP MySQL account. XAMPP commonly uses `root` with an empty password on a local development machine.

4. Start the API and frontend:

   ```bash
   npm run dev
   ```

5. Open **http://localhost:5173**.

The API runs at **http://localhost:4000**. On first start, the API creates the `users` table in the MySQL database and creates the initial administrator if one does not already exist. You can also import `database.sql` in phpMyAdmin first; it is safe to run before starting the API.

## Initial administrator

For a fresh database, the defaults in `.env.example` are:

- Username: `Admin`
- Password: `ChangeThisAdminPassword123`

Change these values in `server/.env` before first startup. The initial admin account is created only when the database has no admin account. Changing the environment values later does not change an already-created admin password.

## Student accounts

New students can select **Create account** on the sign-in page and register with their name, email address, and a password of at least 8 characters. Administrators can also create student accounts from **Student records → Add student**. Student sign-in uses the registered email address.

## Production checklist

This project is a runnable starter implementation, not a production security audit. Before public deployment:

- Use HTTPS and a strong, unique `JWT_SECRET`.
- Replace the default admin password and remove default credentials from deployment documentation.
- Configure `CLIENT_ORIGIN` to the exact deployed frontend origin.
- Add rate limiting, audit logging, backups, and a password-reset process.
- Consider secure, HttpOnly cookies instead of browser local storage for session tokens.
- Review applicable school privacy rules and the Philippine Data Privacy Act before storing real student data.

## API routes

| Method | Route | Access | Purpose |
|---|---|---|---|
| POST | `/api/auth/login` | Public | Sign in |
| POST | `/api/auth/register` | Public | Register a student account |
| GET | `/api/auth/me` | Signed-in | Get current account |
| GET | `/api/students` | Admin | List students |
| POST | `/api/students` | Admin | Create student |
| PUT | `/api/students/:id` | Admin or that student | Update student |
| DELETE | `/api/students/:id` | Admin | Delete student |
| GET | `/api/health` | Public | API health check |
