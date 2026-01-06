# MySQL High Availability with HAProxy and Docker Compose

This project demonstrates a **MySQL High Availability and Load Balancing setup using HAProxy and Docker Compose**.

The goal is to run multiple MySQL instances and place HAProxy in front of them as a load balancer. HAProxy routes traffic between MySQL nodes and helps improve availability in case one node becomes unavailable.

---

## 📁 Project Structure

```
MySQL-HAProxy-DockerCompose/
├── docker-compose.yml        # Main Docker Compose file
├── haproxy/
│   ├── haproxy.cfg           # HAProxy configuration file
│   └── ssl/                  # SSL files (must be created manually)
├── master1/
│   ├── .env                  # Environment variables for MySQL node 1
│   └── my.cnf                # MySQL configuration
├── master2/
│   ├── .env                  # Environment variables for MySQL node 2
│   └── my.cnf                # MySQL configuration
└── README.md
```

---

## ✅ Prerequisites

Make sure the following tools are installed on your system:

- Docker
- Docker Compose

---

## 🚀 How to Run

From the project root directory, run:

```bash
docker compose up -d
```

If you are using an older Docker version:

```bash
docker-compose up -d
```

After startup:
- All MySQL containers will be running
- HAProxy will act as a load balancer in front of MySQL instances

---

## 🔐 SSL Configuration (Important)

You **must create the `ssl` directory manually** and place your SSL files inside it.

### Create SSL directory:
```
haproxy/ssl/
```

### Required files:
```
haproxy/ssl/
├── server.crt   # SSL certificate
└── server.key   # Private key
```

These SSL files are used by HAProxy for secure (TLS) connections.  
Make sure the file names match the ones referenced in `haproxy.cfg`.

---

## 🛠 HAProxy Customization

You can modify the following in `haproxy/haproxy.cfg`:
- Backend servers
- Load balancing algorithm
- Health checks
- Listening ports

HAProxy supports TCP and HTTP load balancing and is widely used in production environments.

---

## 📝 Notes

- This project is a **base setup** for MySQL HA using HAProxy.
- For real-world production use, consider implementing:
  - MySQL replication (Master-Master or Master-Slave)
  - Monitoring and alerting
  - Persistent volumes for MySQL data

---

## 📄 License

This project is provided for educational and testing purposes and is free to use and modify.
