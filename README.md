# BugNexus Community Edition 🚀

![BugNexus Hero Image](bugnexus_hero.png)

> **The high-performance, Sentry-compatible error tracking system for modern engineering teams.**

BugNexus is a self-hostable, efficient, and scalable error tracking platform designed to give you full control over your telemetry data. Written in Go (Backend) and Vue.js (Frontend), it offers lightning-fast ingestion and a premium developer experience without the enterprise price tag.

---

## ✨ Key Features

- **Sentry-Compatible API**: Drop-in replacement for your existing Sentry SDKs.
- **Real-Time Dashboards**: Visualize error spikes and trends as they happen with SSE-powered live updates.
- **ARM64 Native**: Optimized for AWS Graviton and modern cloud infrastructure.
- **Smart Fingerprinting**: Automatically groups related errors using configurable rules.
- **High-Performance Ingestion**: Optimized buffered pipeline capable of handling thousands of events per second.
- **Clean Vue 3 UI**: A sleek, minimal dashboard built for speed and clarity.
- **Role-Based Access Control**: Manage teams, organizations, and project permissions.

---

## 🚀 Quick Start with Docker

Deploy your own BugNexus instance in seconds using Docker Compose.

### 1. Requirements
- Docker & Docker Compose
- MariaDB / MySQL
- Redis (Optional, for caching and rate limiting)
- ClickHouse (For long-term event storage)

### 2. Deployment Options

#### Option A: Docker Compose (Recommended)
Deploy the full stack (App + DBs) in seconds:
```bash
docker-compose up -d
```

#### Option B: Standalone Binary
Download the latest pre-compiled binary for your OS from your private storage.
The binary contains both the backend and frontend. You only need to provide a connection string to your MariaDB instance.
```bash
# Example for Linux
./bugnexus-linux-amd64 --db "user:pass@tcp(localhost:3306)/bugnexus"
```

#### Option C: Custom DockerHub Push
If you want to host your community edition image on DockerHub:

**Windows (PowerShell)**
```powershell
.\scripts\push_dockerhub.ps1
```

**Linux/macOS (Shell)**
```bash
./scripts/push_dockerhub.sh
```

### 3. Architecture
BugNexus uses a decoupled architecture:
- **BugNexus Image**: Contains ONLY the application binary and the embedded frontend.
- **Infrastructure Services**: Databases like MariaDB, Redis, and ClickHouse are **NOT** bundled inside the BugNexus image. You must run them alongside the app (e.g., using `docker-compose`).

---

### 4. Access the Dashboard
Open your browser and navigate to:
`http://localhost:8082`

---

## 🔒 Security & Privacy

We take data sovereignty seriously.
- **Self-Hosted**: Your data never leaves your infrastructure.
- **Obfuscated Assets**: Frontend assets are obfuscated to protect intellectual property in the Community Edition.
- **JWT-Based Auth**: Secure session management and API key rotation.

---

## 📜 Licensing

BugNexus Community Edition is licensed under a custom **Commercial-Prohibited** license.
- ✅ **Free for internal use** in your organization.
- ❌ **Commercial redistribution** or SaaS reselling is prohibited.
- ❌ **No Regress**: Provided "as is" with no warranty.

---

## 🤝 Community & Support

BugNexus is powered by **Nexus Web Tools**.

- [Explore DomainVitals](https://domainvitals.dev) - Insights for your web vitals and SEO.
- [Documentation](https://docs.bugnexus.com)
- [Report a Bug](https://github.com/NexusWebTools/BugNexus/issues)

---

<p align="center">
  Made with ❤️ by the Nexus Web Tools Team
</p>
