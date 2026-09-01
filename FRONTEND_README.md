# Amrish HRMS - Frontend

Modern, responsive React-based frontend for the Amrish Human Resource Management System.

## Features

### 🎨 Modern UI/UX
- Clean, professional design with intuitive navigation
- Responsive layout for desktop, tablet, and mobile devices
- Dark mode support (system-based)
- Smooth animations and transitions

### 🔐 Authentication & Security
- Email/password login with JWT authentication
- Two-factor authentication (MFA) with QR code
- Password reset functionality
- Role-based access control (Super Admin, Admin, Manager, Team Lead, Employee)
- Session management with auto-logout

### 📊 Core Modules
- **Dashboard** - Overview of key metrics and activities
- **Employee Management** - User profiles, departments, designations
- **Attendance System** - Check-in/check-out with QR codes and location tracking
- **Leave Management** - Request, approve, track leave balances
- **Payroll** - View and download payslips
- **Timesheets** - Project-based time tracking and approvals
- **Projects & Tasks** - Project management with sprints and tasks
- **Announcements** - Company-wide and targeted announcements
- **Reports** - Comprehensive HR analytics and reports
- **Settings** - User preferences and system configurations

### 💡 Key Highlights
- Real-time notifications
- Advanced filtering and search
- Excel/PDF export capabilities
- Bulk operations support
- Mobile-responsive design
- Offline capability (PWA ready)

## Tech Stack

- **Framework**: React 19.1.1
- **Build Tool**: Vite 7
- **Routing**: React Router v7
- **State Management**: React Context API + Hooks
- **HTTP Client**: Axios
- **UI Library**: Ant Design (antd)
- **UI Components**: Material-UI (MUI)
- **Additional UI**: Flowbite, DaisyUI, Headless UI
- **Icons**: Ant Design Icons, Material Icons, React Icons, Lucide React, Heroicons
- **Forms**: Formik + Yup validation
- **Date Handling**: Moment.js, date-fns
- **Notifications**: React Hot Toast, React Toastify
- **Charts**: MUI X Data Grid
- **Styling**: CSS Modules + Tailwind CSS + PostCSS
- **JWT Handling**: jwt-decode
- **Organizational Chart**: react-organizational-chart

## Prerequisites

- Node.js (v18 or higher)
- npm or yarn
- Running backend API (see backend README)

## Installation

### 1. Clone the Repository
```bash
git clone <repository-url>
cd hrms-management-system-frontend
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Configure Environment Variables

Create a `.env` file in the root directory:

```env
# API Configuration
VITE_API_URL=http://localhost:3001/api

# For production, use:
# VITE_API_URL=https://hrm.amrish.com/api
```

### 4. Add Company Logo

Add your company logo to the `public` folder:
```
public/company_logo.png
```

Recommended specifications:
- Format: PNG with transparent background
- Dimensions: ~180x60 pixels
- Max size: < 100KB

## Running the Application

### Development Mode
```bash
npm run dev
```
Application runs on `http://localhost:5173`

### Build for Production
```bash
npm run build
```
Builds to `dist/` folder

### Build for Production (with production environment)
```bash
npm run build:prod
```

### Preview Production Build
```bash
npm run preview
```

### Serve Production Build
```bash
npm run serve
```

### Lint Code
```bash
npm run lint
```

### Run Tests
```bash
npm run test          # Run tests once
npm run test:watch    # Run tests in watch mode
```

## Project Structure

```
amrish-hrms-frontend/
├── public/                 # Static assets
│   ├── company_logo.png    # Company logo (add your own)
│   └── vite.svg           # Vite logo
├── src/
│   ├── assets/            # Images, fonts, icons
│   ├── components/        # Reusable components
│   │   ├── common/        # Navbar, Sidebar, Footer, etc.
│   │   ├── layout/        # Layout components
│   │   └── ui/            # Buttons, Inputs, Modals, etc.
│   ├── pages/             # Page components
│   │   ├── auth/          # Login, Register, MFA, ForgotPassword
│   │   ├── dashboard/     # Dashboard pages by role
│   │   ├── attendance/    # Attendance pages
│   │   ├── leaves/        # Leave management
│   │   ├── payroll/       # Payroll & payslips
│   │   ├── payslips/      # Payslip pages
│   │   ├── timesheets/    # Timesheet pages
│   │   ├── projects/      # Project management
│   │   ├── users/         # User management
│   │   ├── announcements/ # Announcements
│   │   ├── reports/       # Reports and analytics
│   │   └── settings/      # Settings pages
│   ├── services/          # API service functions
│   │   ├── api/           # API configurations
│   │   ├── auth.service.js
│   │   ├── user.service.js
│   │   ├── attendance.service.js
│   │   └── ...
│   ├── utils/             # Utility functions
│   │   ├── api.js         # Axios configuration
│   │   ├── auth.js        # Auth utilities (token management)
│   │   └── helpers.js     # Helper functions
│   ├── contexts/          # React contexts
│   │   ├── AuthContext.jsx
│   │   ├── MenuContext.jsx
│   │   └── ...
│   ├── hooks/             # Custom React hooks
│   ├── styles/            # Global styles
│   │   ├── index.css      # Main stylesheet
│   │   ├── App.css        # App-specific styles
│   │   ├── responsive.css # Responsive styles
│   │   ├── breakpoints-visual.css
│   │   └── ...
│   ├── routes/            # Route configurations
│   ├── App.jsx            # Root component with routing
│   ├── App.css            # App-specific styles
│   └── main.jsx           # Entry point
├── dist/                  # Production build (generated)
├── node_modules/          # Dependencies (generated)
├── .env                   # Environment variables (create this)
├── .env.production        # Production environment
├── .gitignore             # Git ignore rules
├── index.html             # HTML template
├── package.json           # Dependencies
├── package-lock.json      # Dependency lock file
├── vite.config.js         # Vite configuration
├── eslint.config.js       # ESLint configuration
├── postcss.config.js      # PostCSS configuration
├── tailwind.config.js     # Tailwind CSS configuration
└── README.md              # This file
```

## Key Features Details

### Authentication Flow
1. User enters email and password
2. System validates credentials
3. If MFA is enabled, user scans QR code
4. User enters 6-digit OTP
5. Upon success, JWT token is stored in session storage
6. All subsequent requests include JWT in Authorization header

### Role-Based Access
Different roles have different permissions:
- **Super Admin**: Full system access
- **Admin**: Manage users, approve payroll
- **Manager**: View team data, approve leaves/timesheets
- **Team Lead**: Manage team members, approve leaves
- **Employee**: View own data, submit requests

### Responsive Design
The application is fully responsive with breakpoints:
- Mobile: < 768px
- Tablet: 768px - 1024px
- Desktop: > 1024px

## API Integration

The frontend communicates with the backend API using Axios.

### Base URL Configuration
Set in `.env` file:
```env
VITE_API_URL=http://localhost:3001/api
```

### Authentication Headers
All authenticated requests include:
```javascript
Authorization: Bearer <jwt_token>
```

### API Endpoints
See backend API documentation for available endpoints.

## Environment Variables

### Development (.env)
```env
VITE_API_URL=http://localhost:3001/api
```

### Production (.env.production)
```env
VITE_API_URL=https://hrm.amrish.com/api
```

## Building for Production

### 1. Update Environment Variables
Edit `.env.production` with your production API URL.

### 2. Build the Application
```bash
npm run build
```

### 3. Deploy the `dist/` Folder
Upload the contents of the `dist/` folder to your web server or hosting platform:
- Netlify
- Vercel
- AWS S3 + CloudFront
- Azure Static Web Apps
- Traditional web hosting

### 4. Configure Web Server
For SPA routing to work correctly, configure your server to redirect all requests to `index.html`.

**Nginx example**:
```nginx
location / {
  try_files $uri $uri/ /index.html;
}
```

**Apache example** (.htaccess):
```apache
RewriteEngine On
RewriteBase /
RewriteRule ^index\.html$ - [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.html [L]
```

## Browser Support

- Chrome/Edge (latest)
- Firefox (latest)
- Safari (latest)
- Mobile browsers (iOS Safari, Chrome Android)

## Performance Optimizations

- Code splitting with React.lazy()
- Image optimization
- Lazy loading for images and routes
- Debounced search inputs
- Virtualized lists for large datasets
- Service worker for caching (PWA)

## Security Best Practices

- JWT tokens stored in sessionStorage (cleared on browser close)
- HTTPS enforced in production
- CORS configured on backend
- XSS protection with input sanitization
- CSRF protection via JWT
- Content Security Policy headers

## Troubleshooting

### Application Won't Start
- Check Node.js version (should be v18+)
- Delete `node_modules` and `package-lock.json`, then run `npm install` again
- Clear npm cache: `npm cache clean --force`
- Ensure Vite is properly installed: `npm install -D vite`

### API Connection Issues
- Verify backend is running
- Check `.env` file has correct API URL
- Check CORS settings on backend
- Verify network connection

### Build Fails
- Check for console errors
- Ensure all dependencies are installed
- Try deleting `node_modules` and reinstalling
- Check for syntax errors in code

### Login Issues
- Clear browser cache and session storage
- Verify backend is running
- Check email domain validation (@amrish.com)
- Verify credentials are correct

## Development Guidelines

### Code Style
- Use functional components with hooks
- Follow React best practices
- Use meaningful variable/function names
- Add comments for complex logic
- Keep components small and focused

### Component Structure
```jsx
// 1. Imports
import React, { useState } from 'react';

// 2. Component
const MyComponent = () => {
  // 3. State and hooks
  const [data, setData] = useState([]);
  
  // 4. Event handlers
  const handleClick = () => {
    // logic
  };
  
  // 5. Render
  return (
    <div>
      {/* JSX */}
    </div>
  );
};

// 6. Export
export default MyComponent;
```

### Git Workflow
1. Create feature branch: `git checkout -b feature/my-feature`
2. Make changes and commit: `git commit -m "Add feature"`
3. Push to remote: `git push origin feature/my-feature`
4. Create pull request
5. After review, merge to main

## Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

## License

This project is proprietary software. All rights reserved.

## Support

For issues or questions:
- Create an issue on GitHub
- Contact: admin@amrish.com

## Changelog

See `REBRANDING_SUMMARY.md` for recent changes.

---

**Made with ❤️ for Amrish HRMS**
