# DevOps Monitoring & Reverse Proxy Stack  
**Traefik · Pi-hole · Prometheus · Grafana · Loki · Promtail · NGINX**

This repository contains a **production-style Docker Compose stack** designed to demonstrate modern **DevOps monitoring, observability, and secure reverse-proxy patterns** using containerized infrastructure.

The stack is intentionally built to be:
-  Secure by default
-  Observable end-to-end
-  Modular and reusable
-  Suitable for homelabs and learning environments
-  Safe to publish publicly (no secrets committed)

---

##  Stack Overview

### Core Capabilities
-  **Traefik** as a reverse proxy with automatic HTTPS
-  **Pi-hole** for DNS filtering and ad blocking
-  **Prometheus** for metrics collection
-  **Grafana** for dashboards and visualization
-  **Loki + Promtail** for centralized log aggregation
-  **NGINX** static site served behind Traefik
-  **BasicAuth + security headers** via Traefik middlewares

All external access is routed through **Traefik** and secured with TLS.

---

##  Services Included

| Service | URL (via Traefik) | Purpose |
|------|------------------|--------|
| Traefik | `https://${TRAEFIK_WEB}` | Reverse proxy & dashboard |
| Pi-hole | `https://${PIHOLE_WEB}` | Network-wide DNS filtering |
| Prometheus | `https://${PROMETHEUS_WEB}` | Metrics scraping |
| Grafana | `https://${GRAFANA_WEB}` | Metrics visualization |
| Static Site | `https://${WEBSITE_WEB}` | NGINX-hosted site |

>  Administrative endpoints are protected using **BasicAuth**.

---

##  Repository Structure

```

.
├── docker-compose.yml
├── traefik.yaml
├── .env
├── config/
│   ├── traefik.yml
│   ├── grafana.yml
│   ├── prometheus-route.yml
│   ├── pihole.yml
│   ├── proxmox.yml
│   ├── middleware.yml
│   └── nginx.conf
├── loki/
│   ├── loki-config.yml
│   └── promtail-config.yml
└── mywebsite/
├── index.html
├── robots.txt
└── favicon.ico

````

> Runtime data, secrets, and certificates are intentionally excluded from version control.

---

##  Security Highlights

-  HTTPS enforced everywhere via Traefik
-  DNS-01 challenge using Cloudflare (no port 80 cert validation)
-  No secrets committed to GitHub
-  BasicAuth protection for admin endpoints
-  Security headers enabled (HSTS, XSS protection, no sniffing)
-  Internal services are **not exposed directly to the internet**

---

## ⚙️ Quick Start

### 1️⃣ Clone the repository
```bash
git clone https://github.com/mikecozier/docker-traefik-stack.git
cd docker-traefik-stack
````

---

### 2️⃣ Create your `.env` file

Use the provided template:

```bash
.env
```

Example values:

```bash
# Domains
TRAEFIK_WEB=traefik.example.com
PIHOLE_WEB=pihole.example.com
PROMETHEUS_WEB=prometheus.example.com
GRAFANA_WEB=grafana.example.com
WEBSITE_WEB=example.com

# Authentication
WEBPASSWORD=change_me
GF_SECURITY_ADMIN_USER=admin
GF_SECURITY_ADMIN_PASSWORD=change_me

# Cloudflare DNS (ACME)
CLOUDFLARE_DNS_API_TOKEN=your_cloudflare_api_token
```

---

### 3️⃣ Launch the stack

```bash
docker compose up -d
```

---

##  DNS & Networking Requirements

* All domains must point to your Docker host
* Cloudflare proxy **enabled** for DNS-01 TLS
* Router forwards:

  * TCP **80**
  * TCP **443**

---

##  Observability Features

### Metrics

* Prometheus scrapes:

  * Node Exporter
  * Container metrics
* Grafana dashboards visualize:

  * Host CPU, memory, disk
  * Container resource usage
  * Network activity

### Logs

* Promtail collects:

  * Docker container logs
  * Host system logs (optional)
* Loki stores and indexes logs centrally
* Logs can be queried directly from Grafana

---

##  Design Philosophy

This stack intentionally mirrors **real-world DevOps patterns**:

* Infrastructure-as-code via Docker Compose
* Centralized ingress & TLS
* Metrics + logs separation
* Least-privilege exposure
* Public-safe configuration templates

It is designed to be **extended**, not monolithic.

---

##  About the Author

**Michael Cozier**
Retired NYPD Sergeant 👮‍♂️
Former U.S. Army Veteran 🎖️
DevOps / Infrastructure Engineer 🖥️

*  GitHub: [https://github.com/mikecozier](https://github.com/mikecozier)
*  LinkedIn: [https://www.linkedin.com/in/mikecozier](https://www.linkedin.com/in/mikecozier)

---

##  Disclaimer

This repository uses **example values only**.
Before deploying in a real environment, replace all placeholders and review security settings.

---

If this repo helped you learn or build something useful, feel free to star it.

```
