# MySQL with HAProxy and Docker Compose (SSL Enabled)

This project provides a **production-ready MySQL deployment using Docker Compose**, with **HAProxy acting as a TCP proxy** and **TLS/SSL enforced** for all database connections.

The architecture is designed to be clean, secure, and extensible, suitable for **enterprise, banking, and regulated environments** where encrypted database traffic and clear separation of concerns are required.

---

## 📁 Project Structure

```
project-root/
├── conf.d/
│   └── mysql.cnf            # MySQL configuration
├── docker-compose.yml       # Docker Compose definition
├── .env                     # Environment variables
├── haproxy/
│   └── haproxy.cfg          # HAProxy configuration
├── logs/                    # MySQL logs
├── mysql/
│   ├── conf.d/              # MySQL config mount
│   └── logs/                # MySQL container logs mount
└── ssl/
    ├── ca.pem               # Certificate Authority
    ├── cert.pem             # Server certificate
    └── key.pem              # Server private key
```

---

## ✅ Prerequisites

Ensure the following components are installed before deployment:

- Docker
- Docker Compose

---

## 🚀 Deployment

From the project root directory, execute:

```bash
docker compose up -d
```

For legacy Docker installations:

```bash
docker-compose up -d
```

Once deployed:
- MySQL starts with custom configuration and persistent storage
- HAProxy exposes MySQL through a controlled TCP entry point
- All client connections are required to use TLS/SSL

---

## 🔐 SSL / TLS Configuration (Mandatory)

You **must create the `ssl` directory manually** and place valid TLS certificates inside it before starting the services.

### Required structure:
```
ssl/
├── ca.pem     # Certificate Authority
├── cert.pem   # Server certificate
└── key.pem    # Server private key
```

These certificates are mounted directly into the MySQL container.  
Because `require_secure_transport = ON` is enabled, **MySQL will refuse non‑SSL connections**.

If the SSL files are missing or invalid, the MySQL container will fail to start.

---

## 🛠 HAProxy Configuration

HAProxy operates in **TCP mode**, acting as a transparent proxy for MySQL traffic without terminating TLS.

You may customize the following parameters in `haproxy/haproxy.cfg`:
- Frontend listening port
- Backend MySQL target
- Timeouts and connection limits
- Health checks (for future multi‑backend expansion)

This design allows seamless scaling to multiple MySQL backends if required.

---

## 📝 Operational Notes

- Configuration, logs, and data are externalized via volumes for maintainability.
- Designed as a **secure baseline** for containerized MySQL deployments.
- Suitable for lab, staging, and controlled production use.
- Can be extended with:
  - Primary / Replica replication
  - Multiple MySQL nodes behind HAProxy
  - Monitoring, alerting, and backup automation

---

## 📄 License

This project is provided for educational and operational reference purposes and is free to use and modify.
