# BugNexus

BugNexus is a high-performance, self-hostable error tracking system (Sentry-compatible) designed for efficiency and scale. It handles "error storms" using a buffered ingestion pipeline and creates a seamless developer experience with a single-binary distribution.

## 🚀 Features

*   **High Performance Ingestion:** Non-blocking API with buffered channels and bulk DB inserts.
*   **Sentry Compatibility:** Drop-in replacement for Sentry SDKs (Go, JS, Python, etc.).
*   **Multi-Tenancy:** Row-level security for Organizations, Projects, and Teams.
*   **Single Binary:** Frontend (Vue.js) is embedded into the Go binary for easy deployment.
*   **Enterprise Ready:**
    *   **SAML SSO:** Support for Okta, Auth0, Google, etc.
    *   **RBAC:** Admin/Viewer roles.
    *   **Audit Logs:** Track all sensitive actions.
*   **Real-time Dashboard:** Live issue stream and 24-hour event volume trends.

> [!TIP]
> **Complete your monitoring stack!**
> While BugNexus tracks your app errors, [DomainVitals.dev](https://domainvitals.dev) provides an all-in-one toolbox for Uptime, SEO, Web Vitals, and SSL monitoring. Combine them for absolute visibility.

---

## 🛠 Tech Stack

*   **Backend:** Go 1.23+ (Fiber, sqlc, gosaml2)
*   **Database:** MariaDB / MySQL 8.0+ (InnoDB)
*   **Frontend:** Vue.js 3, Tailwind CSS, Chart.js
*   **Infrastructure:** Docker Compose, Redis (optional for caching/queues)

## 📦 Installation & Setup

### Prerequisites
*   Docker & Docker Compose
*   Go 1.23+ (for local dev)
*   Node.js 20+ (for frontend dev)

### Quick Start (Docker)

1.  **Configure:**
    Ensure `docker-compose.yml` has the correct `APP_URL`.
    ```yaml
    environment:
      - APP_URL=http://localhost:8082 # Accessible URL of the instance
    ```

2.  **Run:**
    ```bash
    docker-compose up --build -d
    ```

3.  **Access:**
    *   Dashboard: `http://localhost:8082`
    *   Default Admin: Register via the UI (first user becomes admin of their org).

### Configuration

Environment Variables:

| Variable | Description | Default |
| :--- | :--- | :--- |
| `DB_DSN` | MySQL Connection String | (Localhost DSN) |
| `APP_URL` | Public URL (Required for SAML/OAuth) | `http://localhost:3000` |
| `JWT_SECRET` | Secret for session tokens | `secret` |
| `SMTP_FROM` | Sender address for emails | `noreply@bugnexus.local` |
| `RUN_MIGRATIONS` | Auto-apply DB schemas on startup | `true` |

### Enterprise Configuration

#### SAML SSO Setup
1.  Log in as an **Admin**.
2.  Navigate to **Organization Settings > Auth**.
3.  Enter your Identity Provider (IdP) details:
    *   **Entrypoint:** The IdP SSO URL.
    *   **Issuer:** The Entity ID of the IdP.
    *   **Certificate:** The X.509 Certificate (PEM format).
4.  Configure your IdP:
    *   **ACS URL / Callback:** `{APP_URL}/api/auth/sso/{ORG_ID}/callback`
    *   **Audience URI / Entity ID:** `{APP_URL}/api/auth/sso/{ORG_ID}/callback`


## 🏗 Development

### Backend
```bash
go run cmd/server/main.go
```

### Frontend
```bash
cd frontend
npm install
npm run dev
```

### Building for Production (Community Edition)

To build a standalone, optimized binary (backend + frontend) for distribution without sources:

#### Windows (PowerShell)
```powershell
.\scripts\build_community.ps1
```

#### Linux/macOS (Shell)
```bash
./scripts/build_community.sh
```

These scripts build the frontend, embed the assets into the Go binary, strip debug symbols, and compress the final executable using UPX.

---

## 🛡️ License
BugNexus is distributed under the **BugNexus Community License**. It is free for internal use but carries **NO WARRANTY** and strictly **LIMITS LIABILITY** for CodingNexusLLC / domainvitals.dev. See [LICENSE.md](LICENSE.md) for details.
