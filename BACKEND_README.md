# Amrish HRMS - Backend

A comprehensive Human Resource Management System for managing employees, attendance, leave, payroll, timesheets, projects, and HR operations.

## Features

### Core Modules
- 👥 **Employee Management** - Complete employee lifecycle management
- 📅 **Attendance System** - Check-in/check-out with location tracking and QR codes
- 🏖️ **Leave Management** - Leave requests, approvals, balance tracking, and accrual
- 💰 **Payroll System** - Salary calculations, deductions, PDF payslips generation
- ⏰ **Timesheet Tracking** - Project-based time tracking and approval workflow
- 📊 **Project Management** - Projects, tasks, sprints, and team assignments
- 📢 **Announcements** - Company-wide and targeted announcements
- 🔔 **Notifications** - Real-time in-app and email notifications
- 📈 **Reports & Analytics** - Comprehensive HR reports and dashboards
- 🔐 **Role-Based Access Control** - Multi-level permissions (Super Admin, Admin, Manager, Team Lead, Employee)
- 🔑 **MFA Authentication** - Two-factor authentication with QR codes

## Tech Stack

- **Runtime**: Node.js
- **Framework**: Express.js
- **Database**: PostgreSQL
- **ORM**: Sequelize
- **Authentication**: JWT + Bcrypt + Speakeasy (MFA)
- **Email**: Nodemailer
- **PDF Generation**: PDFKit
- **QR Codes**: qrcode library
- **Scheduling**: node-cron
- **Testing**: Jest

## Prerequisites

- Node.js (v14 or higher)
- PostgreSQL (v12 or higher)
- npm or yarn

## Installation

### 1. Clone the Repository
```bash
git clone <repository-url>
cd hrms-management-system-backend
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Configure Environment Variables
```bash
cp .env.example .env
```

Edit `.env` file and fill in your actual values:
- Database credentials
- JWT secret key
- SMTP email configuration
- Encryption keys

### 4. Setup Database

#### Create Database
```sql
CREATE DATABASE amrish_hrms_db;
```

#### Run Migrations
```bash
npx sequelize-cli db:migrate
```

### 5. Create Super Admin (First Time Setup)
```bash
node scripts/create-super-admin.js
```

Default credentials:
- Email: `admin@amrish.com`
- Password: `Password@123`
- Role: `super_admin`

**⚠️ Change these credentials immediately after first login!**

**To retrieve MFA code for login:**
```bash
node scripts/get-mfa-code.js admin@amrish.com
```

This will display the 6-digit MFA code needed for login.

## Running the Application

### Development Mode
```bash
npm run dev
```
Server runs on `http://localhost:3001`

### Production Mode
```bash
npm run prod
```

### Testing Mode
```bash
npm run testing
```

## Scripts

```bash
# Main Scripts
npm start                      # Start server (production)
npm run dev                    # Development with nodemon
npm run prod                   # Production mode
npm run testing                # Testing environment

# Testing
npm test                       # Run tests
npm run test:watch             # Run tests in watch mode
npm run test:coverage          # Generate test coverage report

# Database Management
npm run db:setup               # Complete database setup
npm run db:create              # Create database and tables
npm run db:create-tables       # Create all tables
npm run db:migrate             # Run Sequelize migrations
npm run db:compare             # Compare databases

# Leave Management Scripts
npm run leave:test             # Test leave system
npm run leave:test-calc        # Test leave balance calculation
npm run leave:test-pending     # Test balance with pending leaves
npm run leave:fix-balances     # Fix incorrect balances
npm run leave:find-issues      # Find balance issues
npm run leave:init             # Initialize user leave balances
npm run leave:seed             # Seed leave types
npm run leave:manage           # Manage leave types
npm run leave:cleanup          # Cleanup orphaned balances

# Check-in Management Scripts
npm run checkin:fix-timezone   # Fix timezone in check-ins
npm run checkin:test-timezone  # Test IST timezone
npm run checkin:test-reminders # Test check-in reminders

# Migration Scripts
npm run migrate:production     # Run production auto-leave migration
npm run migrate:verify         # Verify production migration
npm run migrate:testing        # Run testing migration
```

## API Documentation

### Base URL
```
http://localhost:3001/api
```

### Main Endpoints

#### Authentication
- `POST /api/auth/login` - User login
- `POST /api/auth/verify-mfa` - Verify MFA code
- `POST /api/auth/forgot-password` - Password reset request
- `POST /api/auth/reset-password` - Reset password
- `POST /api/auth/refresh-mfa` - Refresh MFA QR code

#### Users
- `GET /api/users` - Get all users
- `GET /api/users/:id` - Get user by ID
- `POST /api/users` - Create user
- `PUT /api/users/:id` - Update user
- `DELETE /api/users/:id` - Delete user

#### Attendance
- `POST /api/attendance/checkin` - Check-in
- `POST /api/attendance/checkout` - Check-out
- `GET /api/attendance/my-records` - Get my attendance
- `GET /api/attendance/users/:userId` - Get user attendance

#### Leave
- `GET /api/leaves` - Get all leave requests
- `POST /api/leaves` - Submit leave request
- `PUT /api/leaves/:id/approve` - Approve leave
- `PUT /api/leaves/:id/reject` - Reject leave
- `GET /api/leaves/my-balance` - Get leave balance

#### Payroll
- `GET /api/payroll` - Get payroll records
- `POST /api/payroll/generate` - Generate payroll
- `GET /api/payroll/:id/payslip` - Download payslip PDF
- `PUT /api/payroll/:id` - Update payroll

#### Timesheets
- `GET /api/timesheets` - Get timesheets
- `POST /api/timesheets` - Submit timesheet
- `PUT /api/timesheets/:id/approve` - Approve timesheet
- `PUT /api/timesheets/:id/reject` - Reject timesheet

#### Projects
- `GET /api/projects` - Get all projects
- `POST /api/projects` - Create project
- `PUT /api/projects/:id` - Update project
- `DELETE /api/projects/:id` - Delete project

#### Announcements
- `GET /api/announcements` - Get announcements
- `POST /api/announcements` - Create announcement
- `PUT /api/announcements/:id` - Update announcement
- `DELETE /api/announcements/:id` - Delete announcement

## Project Structure

```
amrish-hrms-backend/
├── config/                 # Configuration files (database, etc.)
├── controllers/            # Route controllers (30+ controllers)
├── models/                 # Sequelize models (43 tables)
├── routes/                 # API routes
├── services/               # Business logic services
│   ├── emailService.js     # Email sending service
│   ├── pdfService.js       # PDF generation service
│   ├── attendanceMonitor.js # Attendance monitoring
│   └── ...
├── middleware/             # Custom middleware
│   ├── auth.js             # JWT authentication
│   ├── roleCheck.js        # Role-based access control
│   └── ...
├── utils/                  # Helper utilities
│   ├── encryption.js       # AES encryption utilities
│   ├── validation.js       # Input validation
│   └── ...
├── migrations/             # Database migrations (Sequelize)
├── jobs/                   # Scheduled jobs (node-cron)
│   ├── dailyAttendanceJob.js
│   ├── earnedLeaveAccrualJob.js
│   └── ...
├── tests/                  # Unit & integration tests
├── docs/                   # Documentation
│   ├── SYSTEM_ARCHITECTURE.md
│   ├── LOP_SYSTEM.md
│   ├── checkin-reminders.md
│   └── ...
├── public/                 # Static files
│   ├── payslips/          # Generated payslips
│   ├── qrcodes/           # QR codes for check-in
│   └── ...
├── scripts/                # Setup & maintenance scripts
│   ├── create-super-admin.js
│   ├── setup-database-complete.js
│   ├── get-mfa-code.js
│   └── ...
├── backups/                # Database backups
├── logs/                   # Application logs
├── data-templates/         # Data templates
├── server.js               # Main application entry point
├── .env.example            # Environment variables template
├── .env                    # Environment variables (create this)
├── .dockerignore           # Docker ignore file
├── Dockerfile              # Docker configuration
├── .gitlab-ci.yml          # GitLab CI/CD pipeline
├── .sequelizerc            # Sequelize CLI configuration
├── package.json            # Dependencies & scripts
└── README.md               # This file
```

## User Roles & Permissions

| Role | Permissions |
|------|------------|
| **Super Admin** | Full system access, manage all users, settings, and data |
| **Admin** | Manage users, view all data, approve payroll |
| **Manager** | View team data, approve leaves/timesheets |
| **Team Lead** | Manage team members, approve leaves/timesheets |
| **Employee** | Submit leaves, timesheets, view own data |

---

## Database Schema

The system uses **43 tables** in PostgreSQL to manage all HR operations:

### **1. User Management (1 table)**
- **Users** - Employee information, roles, hierarchy (teamLead, manager)

### **2. Attendance & Check-in (3 tables)**
- **Checkins** - QR code check-in/check-out with location
- **DailyAttendance** - Daily attendance records and work hours
- **AttendanceCorrections** - Attendance correction requests

### **3. Leave Management (7 tables)**
- **Leaves** - Leave requests and approvals
- **LeaveTypes** - Leave categories (Casual, Sick, Earned, etc.)
- **ActiveLeaveTypes** - Currently active leave types
- **UserLeaveBalances** - User-wise leave balance per type
- **LeaveBalanceLogs** - Leave balance change history
- **LeaveAccrualHistories** - Leave accrual tracking
- **OptionalHolidays** - Optional/restricted holidays

### **4. Earned Leave System (4 tables)**
- **EarnedLeavePolicies** - Earned leave policy rules
- **EarnedLeaveAccrualTiers** - Tier-based accrual rates
- **EarnedLeaveAccrualLogs** - Monthly accrual logs
- **EarnedLeavePeriods** - Leave accrual periods

### **5. Payroll & Salary (8 tables)**
- **Payslips** - Generated payslips with encrypted salary data
- **PayrollHistories** - Payroll processing history
- **PayrollSettings** - Organization payroll configuration
- **PayrollEarnings** - Custom earnings (bonuses, allowances)
- **PayrollDeductions** - Custom deductions (LOP, loans)
- **SalaryStructures** - Salary component definitions
- **UserSalaries** - User-wise salary assignments
- **DeductionTypes** - Deduction categories

### **6. Projects & Tasks (6 tables)**
- **Projects** - Project information and status
- **ProjectCodes** - Project billing codes
- **Sprints** - Agile sprint management
- **Tasks** - Task assignments and tracking
- **Timesheets** - Project-based timesheet entries
- **BillingTimesheets** - Billable hours tracking
  - **BillingTimesheetSubmissions** - Submission tracking

### **7. Announcements (5 tables)**
- **Announcements** - Company-wide announcements
- **AnnouncementRecipients** - User-specific recipients
- **AnnouncementGroups** - Announcement distribution groups
- **AnnouncementGroupMembers** - Group membership
- **AnnouncementTeamRecipients** - Team-based recipients

### **8. Organization (3 tables)**
- **Departments** - Department information
- **Designations** - Job titles and levels
- **OfficeSettings** - Organization-wide settings

### **9. System & Notifications (3 tables)**
- **Notifications** - In-app notification system
- **Menus** - Dynamic menu structure
- **RoleMenus** - Role-based menu access

### **10. Financial (1 table)**
- **Reimbursements** - Expense reimbursement requests

### **Key Database Features:**
- ✅ **43 total tables** managing all HR operations
- ✅ **Foreign key relationships** ensuring data integrity
- ✅ **Encrypted sensitive data** (salary, PAN, bank details)
- ✅ **Self-referencing relationships** (org hierarchy)
- ✅ **JSON fields** for flexible data storage
- ✅ **Enum types** for status and role management
- ✅ **Timestamps** on all tables (createdAt, updatedAt)
- ✅ **Soft deletes** via isActive flags
- ✅ **Indexes** on frequently queried columns
- ✅ **Sequelize migrations** for version control

### **Database Setup:**
```bash
# Create database
createdb amrish_hrms_db

# Run all migrations
npx sequelize-cli db:migrate

# Seed initial data (if needed)
node scripts/seed-initial-data.js
```

---

## User Roles & Permissions (Detailed)

## Email Configuration

The system sends emails for:
- Welcome notifications
- Leave approvals/rejections
- Timesheet approvals/rejections
- Announcements
- Password resets
- Task assignments
- Check-in/checkout reminders

Configure SMTP settings in `.env` file.

## Security Features

- ✅ JWT-based authentication
- ✅ Two-factor authentication (MFA)
- ✅ Password hashing (bcrypt)
- ✅ Role-based access control
- ✅ Email domain validation (`@amrish.com`)
- ✅ Payroll data encryption (AES-256)
- ✅ SQL injection protection (Sequelize ORM)
- ✅ Rate limiting
- ✅ Helmet.js security headers

## Scheduled Jobs

The system runs automated jobs using node-cron:

- **Daily Attendance Job** - Auto-marks absent employees at end of day
- **Leave Accrual Job** - Monthly earned leave credit calculation
- **Check-in Reminders** - Sends reminders for users who haven't checked in

## Testing

```bash
# Run all tests
npm test

# Run tests in watch mode
npm run test:watch

# Generate coverage report
npm run test:coverage
```

## Docker Support

### Build Docker Image
```bash
docker build -t amrish-hrms-backend .
```

### Run Container
```bash
docker run -p 3001:3001 --env-file .env amrish-hrms-backend
```

## Troubleshooting

### Database Connection Issues
- Verify PostgreSQL is running
- Check database credentials in `.env`
- Ensure database exists
- Check network/firewall settings

### Migration Errors
```bash
# Reset migrations (CAUTION: Destroys data)
npx sequelize-cli db:migrate:undo:all
npx sequelize-cli db:migrate
```

### Email Not Sending
- Verify SMTP credentials
- Check SMTP host/port
- Enable "Less secure apps" for Gmail
- Use App Passwords for Gmail with 2FA

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is proprietary software. All rights reserved.

## Support

For issues or questions:
- Create an issue on GitHub
- Contact: admin@amrish.com

## Changelog

See `REBRANDING_SUMMARY.md` for recent changes and `REMOVED_FILES.md` for cleanup details.

---

**Made with ❤️ for Amrish HRMS**
