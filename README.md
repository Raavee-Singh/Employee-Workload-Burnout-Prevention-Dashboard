# Equipoise

Equipoise is an employee workload and burnout-prevention dashboard for managers.

## Requirements

- Node.js 20+
- Java 25
- Maven 3.9+

## Run locally

1. Start the backend:

   ```powershell
   cd backend
   mvn spring-boot:run
   ```

   The Spring Boot API runs at `http://localhost:8080/api`. The default `dev` profile uses an H2 in-memory database and seeds sample workspace data at startup.

2. Configure and start the frontend in a second terminal:

   ```powershell
   cd frontend
   Copy-Item .env.example .env
   npm install
   npm run dev
   ```

   Vite serves the app at `http://localhost:5173`.

3. Sign in with the seeded manager account:

   - Email: `manager@equipoise.com`
   - Password: `Password@123`

## Environment variables

Frontend values are read from `frontend/.env`:

| Variable | Default | Description |
|---|---|---|
| `VITE_API_URL` | `http://localhost:8080/api` | Backend API base URL |
| `VITE_USE_MOCK` | `false` in `.env.example` | Set to `true` to use the local mock service data |

Backend configuration uses Spring environment variables:

| Variable | Default / profile | Description |
|---|---|---|
| `SPRING_PROFILES_ACTIVE` | `dev` | `dev` uses H2; `prod` uses PostgreSQL |
| `JWT_SECRET` | Development-only key | Set a strong secret in production |
| `SPRING_DATASOURCE_URL` | Required in `prod` | PostgreSQL JDBC URL |
| `SPRING_DATASOURCE_USERNAME` | Required in `prod` | PostgreSQL username |
| `SPRING_DATASOURCE_PASSWORD` | Required in `prod` | PostgreSQL password |

The production profile requires a database and JWT secret to be supplied through environment variables. Do not use the development JWT key in production.

## Build and verify

```powershell
cd frontend
npm run build

cd ..\backend
mvn clean package
```

The API contract is documented in [`API_CONTRACT.md`](./API_CONTRACT.md). OpenAPI UI is available at `http://localhost:8080/swagger-ui.html` while the backend is running.

Verification results and manual coverage limits are documented in [`TEST_REPORT.md`](./TEST_REPORT.md).
