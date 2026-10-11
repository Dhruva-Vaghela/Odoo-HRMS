 # Dayflow HRMS

 Dayflow is a web-based Human Resource Management System for managing everyday office employee operations. It provides a shared workspace for administrators and HR staff to manage people and HR processes, while employees can access their own work information.

 ## Features

 - Role-based access for administrators, HR staff, and employees
 - Dashboard views for HR operations and employees
 - Employee directory, employee records, and profile management
 - Attendance check-in, check-out, and attendance monitoring
 - Leave requests and approval workflows
 - Payroll records and payment status
 - Authenticated API requests with access and refresh tokens

 Available actions depend on the signed-in user's role.

 ## Technology Stack

 | Area | Technologies |
 | --- | --- |
 | Frontend | React 19, Vite 7, React Router 7 |
 | UI | Material UI 7, Emotion, MUI X Data Grid and Date Pickers |
 | Charts and forms | Recharts, React Hook Form, Day.js |
 | Backend | Node.js, Express 4 |
 | Database and ORM | PostgreSQL 15, Prisma 5 |
 | Authentication and security | JWT, bcrypt, Helmet, CORS, express-rate-limit, express-validator |
 | Development and deployment | ESLint 9, Docker Compose |

 ## Requirements

 - Node.js 18 or newer and npm
 - PostgreSQL 12 or newer for a local backend setup, or Docker Desktop for the containerized database and backend

 ## Run Locally

 ### 1. Install frontend dependencies

 From the repository root:

 ```bash
 npm install
 ```

 ### 2. Configure and start the backend

 Install backend dependencies:

 ```bash
 cd backend
 npm install
 ```

 Create `backend/.env` with your PostgreSQL connection string and development secrets:

 ```env
 PORT=5000
 NODE_ENV=development
 DATABASE_URL="postgresql://USER:PASSWORD@localhost:5432/dayflow_db?schema=public"
 JWT_ACCESS_SECRET=replace-with-a-long-random-secret
 JWT_REFRESH_SECRET=replace-with-a-different-long-random-secret
 JWT_ACCESS_EXPIRES_IN=15m
 JWT_REFRESH_EXPIRES_IN=7d
 CORS_ORIGIN=http://localhost:5173
 ```

 Create the `dayflow_db` database in PostgreSQL, then generate the Prisma client, apply migrations, seed demo data, and start the API:

 ```bash
 npm run db:generate
 npm run db:migrate
 npm run db:seed
 npm run dev
 ```

 The API runs at `http://localhost:5000`; its base path is `http://localhost:5000/api`.

 ### 3. Start the frontend

 In a second terminal, from the repository root:

 ```bash
 npm run dev
 ```

 Open the Vite URL shown in the terminal, usually `http://localhost:5173`. The frontend uses `http://localhost:5000/api` by default. To use another API address, set `VITE_API_BASE_URL`, for example in a root `.env.local` file:

 ```env
 VITE_API_BASE_URL=http://localhost:5000/api
 ```

 ## Run with Docker

 Docker Compose starts PostgreSQL and the backend. From the repository root:

 ```bash
 docker-compose up -d --build
 ```

 The Compose configuration maps the backend to `http://localhost:5002` on your host and PostgreSQL to port `5432`. Start the frontend separately with `npm install` and `npm run dev` from the repository root. When using this Docker backend, configure the frontend API URL as `http://localhost:5002/api`.

 See [README-DOCKER.md](README-DOCKER.md) for Docker logs, database access, and troubleshooting. The Compose file contains development credentials and secrets; replace them before using this setup outside local development.

 ## Demo Accounts

 Seed the database with `npm run db:seed` from `backend/`, then sign in with one of these accounts:

 | Role | Email | Password |
 | --- | --- | --- |
 | Administrator | `admin@dayflow.com` | `Password123!` |
 | HR | `hr@dayflow.com` | `Password123!` |
 | Employee | `john.doe@dayflow.com` | `Password123!` |
 | Employee | `jane.smith@dayflow.com` | `Password123!` |

 These are development-only demo credentials. Do not use them in a production environment.

 ## Useful Commands

 Run these from the repository root unless otherwise noted:

 | Command | Purpose |
 | --- | --- |
 | `npm run dev` | Start the frontend development server |
 | `npm run build` | Build the frontend for production |
 | `npm run lint` | Lint the frontend source |
 | `npm run preview` | Preview the production frontend build |
 | `npm run dev` in `backend/` | Start the backend with automatic restarts |
 | `npm run start` in `backend/` | Start the backend |
 | `npm run db:migrate` in `backend/` | Create and apply a Prisma migration |
 | `npm run db:seed` in `backend/` | Add demo users and sample HR data |
 | `npm run db:studio` in `backend/` | Open Prisma Studio |

 ## Project Structure

 ```text
 .
 ├── backend/
 │   ├── prisma/          # Database schema, migrations, and seed data
 │   └── src/             # Express API, routes, services, and validation
 ├── public/              # Static frontend assets
 └── src/
	 ├── components/      # Shared UI components
	 ├── context/         # Authentication context
	 ├── layouts/         # Application layouts
	 ├── pages/           # Dashboard and HRMS screens
	 └── utils/           # API client and helpers
 ```

 ## Documentation

 - [Backend API documentation](backend/API_DOCUMENTATION.md)
 - [Docker setup and troubleshooting](README-DOCKER.md)

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react) uses [Babel](https://babeljs.io/) (or [oxc](https://oxc.rs) when used in [rolldown-vite](https://vite.dev/guide/rolldown)) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh

## React Compiler

The React Compiler is not enabled on this template because of its impact on dev & build performances. To add it, see [this documentation](https://react.dev/learn/react-compiler/installation).

## Expanding the ESLint configuration

If you are developing a production application, we recommend using TypeScript with type-aware lint rules enabled. Check out the [TS template](https://github.com/vitejs/vite/tree/main/packages/create-vite/template-react-ts) for information on how to integrate TypeScript and [`typescript-eslint`](https://typescript-eslint.io) in your project.
