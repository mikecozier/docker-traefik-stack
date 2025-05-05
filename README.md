# 🐳 DevOps Monitoring & Filtering Stack with Traefik, Pi-hole, Prometheus, Grafana & Netdata

This Docker Compose stack sets up a **secure and observable home server** infrastructure featuring:

- 🔒 Reverse proxy with **Traefik**
- 📡 DNS filtering via **Pi-hole**
- 📊 Metrics collection using **Prometheus**
- 📈 Dashboards with **Grafana**
- 📟 Real-time system monitoring via **Netdata**
- 🌐 A static site using **NGINX**

---

## 📦 Services Included

| Service     | URL (via Traefik + Cloudflare)                 | Purpose                               |
|-------------|------------------------------------------------|----------------------------------------|
| Traefik     | `https://${TRAEFIK_WEB}`                       | Reverse proxy + Dashboard (auth)       |
| Pi-hole     | `https://${PIHOLE_WEB}`                        | DNS filtering and ad-blocking          |
| Prometheus  | `https://${PROMETHEUS_WEB}`                    | Metrics scraping                       |
| Grafana     | `https://${GRAFANA_WEB}`                       | Metrics dashboard                      |
| Netdata     | `https://${NETDATA_WEB}`                       | Real-time system health                |
| Static Site | `https://${WEBSITE_WEB}`                       | Your NGINX-hosted site                 |

> 🔐 Most endpoints are protected via **BasicAuth**.

---

## 🚀 Quick Start

### 1. Clone this repository

```bash
git clone https://github.com/yourusername/devops-stack.git
cd devops-stack
````

### 2. Create a `.env` file

```env
# Domains
TRAEFIK_WEB=traefik.example.com
PIHOLE_WEB=pihole.example.com
PROMETHEUS_WEB=prometheus.example.com
NETDATA_WEB=netdata.example.com
GRAFANA_WEB=grafana.example.com
WEBSITE_WEB=example.com

# Auth
TRAEFIK_AUTH_USERPASS=admin:$(htpasswd -nbB admin your_password | cut -d ':' -f2)
WEBPASSWORD=your_pihole_password
GF_SECURITY_ADMIN_USER=admin
GF_SECURITY_ADMIN_PASSWORD=your_grafana_password

# Cloudflare DNS (for Traefik certs)
CLOUDFLARE_DNS_API_TOKEN=your_cloudflare_token

# Netdata Cloud
NETDATA_CLAIM_TOKEN=your_netdata_claim_token
```

### 3. Launch the stack

```bash
docker compose up -d
```

---

## ⚙️ DNS + Traefik Setup

* All traffic is routed through **Traefik** using **Cloudflare DNS-01 challenge** for automatic SSL.
* Make sure your subdomains (`*.example.com`) are proxied in **Cloudflare**.
* Required ports:

  * TCP 80 & 443 must be **forwarded** from your router to your Docker host.

---

## 📊 Monitoring Highlights

* **Prometheus** scrapes metrics from Node Exporter, Netdata, and more.
* **Grafana** visualizes system & container stats (import dashboards by ID: `15334`, `10301`, etc.)
* **Netdata** offers live CPU, memory, network, disk, and log monitoring.
* **Pi-hole** filters ads & trackers across your entire network.

---

## 🔐 Security Features

* 🔐 All services exposed through Traefik are **TLS secured** with Let's Encrypt.
* 🧱 Services like Traefik, Prometheus, and Netdata are **BasicAuth protected**.
* 🔍 DNS queries routed through Pi-hole for ad & tracker blocking.

---

## 📁 Directory Structure

```bash
.
├── docker-compose.yaml
├── .env
├── config/
│   └── traefik.yaml
├── etc-pihole/
├── etc-dnsmasq.d/
├── mywebsite/          # Your NGINX site
└── netdata-config/
```

---

## 👮‍♂️ Built by

**Michael Cozier**
Retired NYPD Sergeant 👮 • US Army Veteran 🎖️ • DevOps Engineer 🖥️
🔗 [LinkedIn](https://www.linkedin.com/in/michaelcozier)
📦 [GitHub](https://github.com/mikecozier)
