# Amrish HRMS — Human Resource Management System

A full-stack Human Resource Management System designed to manage employees, attendance, leave, payroll, timesheets, projects, announcements, notifications, reports, and HR operations.

## Project Architecture

The HRMS application is maintained as three repositories:

| Repository | Purpose | Technology |
|---|---|---|
| `hrms-management-system` | Main project / documentation | Project overview |
| `hrms-management-system-backend` | REST API and business logic | Node.js, Express.js, PostgreSQL |
| `hrms-management-system-frontend` | Web application | React, Vite, JavaScript |

The backend and frontend are intentionally maintained as separate repositories so they can be developed, versioned, and deployed independently.

## Main Features

- Employee Management
- Attendance and QR Check-in/Check-out
- Location-based attendance tracking
- Leave Management and leave balances
- Payroll and PDF payslips
- Timesheet Management
- Project and Task Management
- Sprint Management
- Announcements
- Real-time notifications
- Reports and analytics
- Role-Based Access Control
- MFA / Two-Factor Authentication
- Password reset
- Reimbursements
- Organization and department management

## User Roles

- **Super Admin** — Full system access
- **Admin** — User management and payroll administration
- **Manager** — Team data and approvals
- **Team Lead** — Team management and approvals
- **Employee** — Personal HR operations and requests

## Technology Stack

### Backend

- Node.js
- Express.js
- PostgreSQL
- Sequelize ORM
- JWT
- Bcrypt
- Speakeasy MFA
- Nodemailer
- PDFKit
- QRCode
- node-cron
- Jest

The backend contains 43 PostgreSQL tables covering the major HR operations and uses migrations for database version control.

### Frontend

- React 19
- Vite 7
- React Router
- Axios
- Ant Design
- Material UI
- Tailwind CSS
- Formik
- Yup
- React Context API
- JavaScript

## Repository Setup

Clone the repositories separately:

```bash
git clone <main-repository-url>
git clone <backend-repository-url>
git clone <frontend-repository-url>
```

### Backend

```bash
cd hrms-management-system-backend
npm install
cp .env.example .env
npx sequelize-cli db:migrate
npm run dev
```

Backend development API:

```text
http://localhost:3001/api
```

### Frontend

```bash
cd hrms-management-system-frontend
npm install
```

Create `.env`:

```env
VITE_API_URL=http://localhost:3001/api
```

Start the frontend:

```bash
npm run dev
```

Frontend development URL:

```text
http://localhost:5173
```

## Frontend ↔ Backend Flow

```text
User
  |
  v
React Frontend
  |
  | Axios / REST API
  v
Node.js + Express Backend
  |
  | Sequelize ORM
  v
PostgreSQL Database
```

Authentication uses JWT. When MFA is enabled, the user completes the MFA verification flow before accessing protected resources.

## Production Deployment

The frontend and backend can be deployed independently.

### Backend

The backend supports Docker deployment:

```bash
docker build -t amrish-hrms-backend .
docker run -p 3001:3001 --env-file .env amrish-hrms-backend
```

### Frontend

Build the production application:

```bash
npm run build
```

The generated `dist/` folder can be deployed to a web hosting platform or static hosting service.

The frontend README documents deployment options including Netlify, Vercel, AWS S3 + CloudFront, Azure Static Web Apps, and traditional web servers.

## Documentation

- [Backend README](./BACKEND_README.md)
- [Frontend README](./FRONTEND_README.md)

The detailed backend documentation covers installation, database setup, API endpoints, migrations, scheduled jobs, security, testing, Docker, and troubleshooting.

The detailed frontend documentation covers UI features, authentication flow, API integration, environment variables, production builds, responsive design, performance, security, and troubleshooting.

## Access to Source Code

The source-code repositories may be private.

If you are an HR/recruiter, interviewer, client, or reviewer and need access to the private source code for technical evaluation, please contact:

**amirthalingamamrish18@gmail.com**

Please send an access request with your name, organization, and GitHub username. Repository access can then be provided where appropriate.

## Security

Do not commit:

- `.env` files
- Database passwords
- JWT secrets
- SMTP passwords
- API keys
- Production credentials
- Private certificates

Use `.env.example` files for configuration templates.

## License

This project is proprietary software. All rights reserved.

## Author

**Amrish A L**

Full Stack Developer
