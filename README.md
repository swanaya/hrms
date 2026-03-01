# HRMS Portal

A lightweight, enterprise-grade Human Resource Management System for managing employee records and tracking daily attendance. Built to provide a highly professional, production-ready interface (using Shadcn UI and GSAP animations) and strict RESTful APIs without feature bloat.

## Project Overview

This project fulfills the full-stack HRMS assignment requirements. It provides an intuitive, admin-facing dashboard allowing for the seamless execution of core HR operations:

1. **Employee Management**: Add new employees, view comprehensive rosters, and delete personnel.
2. **Attendance Tracking**: Mark daily presence (Present/Absent), view individual historical logs, and access a global company-wide attendance summary.
3. **Bonus Features Implemented**:
   - Total Present Days are calculated and displayed per employee.
   - Attendance records can be filtered by employee using a fully searchable dropdown, and by clicking names in the employee data table.
   - Global dashboard summary presenting recent updates across the company.

## Tech Stack Used

**Frontend Setup**:

- **Framework**: React.js with Vite
- **Styling**: TailwindCSS (v3.4.1), Custom Shadcn UI architecture (Card, Label, Input, Button)
- **Animations**: GSAP (GreenSock Animation Platform) for fluid enter animations.
- **Icons**: Lucide React
- **Package Manager**: Bun

**Backend Setup**:

- **Framework**: FastAPI (Python 3.10+)
- **Database**: PostgreSQL
- **ORM**: SQLAlchemy
- **Data Validation**: Pydantic

## Steps to Run the Project Locally

To run the application locally, you will need two terminal tabs open—one for the backend and one for the frontend.

### 1. Backend Setup

Open a terminal and navigate to the backend directory:

```bash
cd hrms/backend
```

Create a virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install the dependencies:

```bash
pip install -r requirements.txt
```

Create an environment file:
Ensure you create a `.env` file in the `hrms/backend` directory containing the database credentials:

```env
DATABASE_URL=postgresql-url
PORT=3009
```

Run the backend server:

```bash
python -m app.main
```

The FastAPI backend will start running at `http://localhost:3009`.
The Interactive API documentation is available at `http://localhost:3009/docs`.

### 2. Frontend Setup

Open a new terminal and navigate to the frontend directory:

```bash
cd hrms/frontend
```

Install the dependencies using Bun:

```bash
bun install
```

Create an environment file:
Ensure you create a `.env` file in the `hrms/frontend` directory containing the backend URL:

```env
VITE_API_BASE_URL=http://localhost:3009
```

Run the frontend development server:

```bash
bun run dev
```

The frontend will start running at `http://localhost:7040`. Navigate to this URL in your browser to access the application.

## Deployment Guidelines

This repository is completely structured and ready for production deployment.

### Deploying the Frontend (Vercel / Netlify)

1. Connet your GitHub repository to Vercel/Netlify.
2. Set the Root Directory to `hrms/frontend`.
3. The Build Command should be `bun run build` (or `npm run build` if using NPM).
4. The Output Directory should be `dist`.
5. **Crucial setup**: Add an Environment Variable in the deployment dashboard for `VITE_API_BASE_URL` pointing to your hosted Backend API URL.

### Deploying the Backend (Render / Railway)

1. Connect via Render/Railway.
2. Set the Root Directory to `hrms/backend`.
3. Set the Build Command to `pip install -r requirements.txt`.
4. Set the Start Command to `python -m app.main` or `uvicorn app.main:app --host 0.0.0.0 --port $PORT`.
5. **Crucial setup**: Add Environment Variables for `DATABASE_URL` (pointing to your live PostgreSQL instance) and `PORT`.

## Assumptions & Limitations

- The application uses a single implicit Admin view. Authentication is simulated through a purely visual login page per the project constraints ("Assume a single admin user (no authentication required)").
- Pagination is currently omitted to retain the lightweight scope of the 'Lite' objective. Large datasets load sequentially.
- Local timezone formatting is implicitly handled by the HTML `<input type="date">` and string comparisons. For a larger distributed company, UTC normalization would be integrated.
