# 🏥 Medical Imaging PACS Portal - Backend API

Robust RESTful API and DICOM PACS proxy gateway designed for high-performance medical imaging management, secure patient access, and clinical reporting.

---

## 🎯 Architecture & Technologies

- **Runtime**: Node.js (ES Modules)
- **Framework**: Express.js
- **Database**: PostgreSQL (hosted on [Neon](https://neon.tech))
- **ORM**: Prisma Client & Migrations
- **PACS Server**: [Orthanc](https://www.orthanc-server.com/) (DICOM Store, Query/Retrieve, Stone Web Viewer)
- **Authentication**: JWT (JSON Web Tokens) with bcrypt password hashing
- **Proxy Gateway**: Dynamic tokenized reverse proxy isolating Orthanc PACS from direct public exposure
- **Mailing**: Resend API for transactional communications

---

## 🚀 Key Responsibilities

1. **Role-Based Access Control (RBAC)**: Enforces permission boundaries across `ADMIN`, `DOCTOR`, and `PATIENT` roles.
2. **DICOM PACS Secure Gateway**: Intercepts requests to the PACS server, validating temporary access tokens so patients only view their authorized studies.
3. **Clinical Studies & Reporting**: Manages medical study metadata, radiologist findings, diagnosis notes, and downloadable medical report PDFs.
4. **DICOM Web & Stone Viewer Integration**: Streams medical instances directly to web clients with zero latency and high compression.

---

## ⚙️ Configuration & Environment

Copy the example environment file and configure your credentials:

```bash
cp .env.example .env
```

### Environment Variables Reference

| Variable | Description |
| :--- | :--- |
| `DATABASE_URL` | Neon PostgreSQL pooled connection string |
| `PORT` | API server port (default: `3000`) |
| `JWT_SECRET` | Secret key for signing authentication tokens |
| `ORTHANC_URL` | Internal HTTP address of the Orthanc PACS server |
| `ORTHANC_USER` | HTTP Basic Auth username for Orthanc |
| `ORTHANC_PASS` | HTTP Basic Auth password for Orthanc |
| `RESEND_API_KEY` | Transactional email provider API key |
| `RESEND_FROM_EMAIL` | Verified sender email address |
| `FRONTEND_URL` | Authorized client origin for CORS policies |
| `NODE_ENV` | Application environment (`development` \| `production`) |

---

## 🛠️ Installation & Execution

```bash
# 1. Install dependencies
npm install

# 2. Generate Prisma Client
npx prisma generate

# 3. Start development server
npm run dev

# 4. Start production server
npm start
```

---

## 📡 Core API Endpoints

### Authentication
- `POST /api/auth/login` - Authenticate user credentials and issue signed JWT.
- `GET /api/auth/me` - Retrieve current session details and assigned role.

### Users & Patients (Admin / Staff)
- `GET /api/users` - Paginated user directory with role and search filters.
- `POST /api/users` - Register a new patient or clinical staff member.
- `GET /api/users/:id` - Fetch user profile by ID.
- `PUT /api/users/:id` - Update user information.
- `DELETE /api/users/:id` - Remove user account.

### Medical Studies & DICOM
- `GET /api/studies` - List available studies filtered by patient, doctor, date range, or study type.
- `POST /api/studies` - Register new study metadata.
- `GET /api/studies/:id` - Retrieve detailed study metadata and associated DICOM instances.

### Clinical Reports
- `GET /api/reports` - List diagnostic reports.
- `POST /api/reports` - Create diagnostic report for a specific study.
- `GET /api/reports/:id` - Retrieve report and download signed PDF.

### Orthanc PACS Proxy
- `/api/orthanc/pacs/*` - Reverse proxy with tokenized authorization for Stone Web Viewer and WADO-RS endpoints.

---

## 🔒 Security Measures

- **No Hardcoded Secrets**: All credentials, tokens, and endpoints are injected via environment variables.
- **Data Isolation**: Patients can never query or access studies outside their own clinical records.
- **CORS Protection**: Access strictly constrained to authorized client origins.
