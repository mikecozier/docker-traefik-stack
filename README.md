## 🐳 **DevOps Monitoring & Filtering Stack**

A secure and observable home server setup using Docker Compose with:

* 🔒 **Traefik:** Reverse proxy with HTTPS
* 📡 **Pi-hole:** DNS filtering and ad blocking
* 📊 **Prometheus:** Metrics scraping
* 📈 **Grafana:** Custom dashboards
* 📟 **Netdata:** Real-time monitoring
* 🌐 **NGINX:** Static website hosting

### 📦 **Services Included:**

| Service     | URL                            | Purpose                          |
| ----------- | ------------------------------ | -------------------------------- |
| Traefik     | https://traefik.example.com    | Reverse proxy + Dashboard (auth) |
| Pi-hole     | https://pihole.example.com     | DNS filtering and ad-blocking    |
| Prometheus  | https://prometheus.example.com | Metrics scraping                 |
| Grafana     | https://grafana..example.com   | Metrics dashboard                |
| Netdata     | https://netdata.example.com    | Real-time system health          |
| Static Site | https://example.com            | NGINX-hosted site                |

### 🚀 **Quick Start:**

1. Clone the repo:

   ```
   git clone https://github.com/mikecozier/docker-traefik-stack.git
   cd docker-traefik-stack
   ```
2. Configure environment variables in `.env`
3. Launch the stack:

   ```
   docker compose up -d
   ```
4. Access services via secured subdomains.

### 🔐 **Security:**

* TLS secured via Let’s Encrypt (Cloudflare DNS challenge)
* BasicAuth for sensitive dashboards
* DNS filtering with Pi-hole

### 📊 **Monitoring:**

* Prometheus + Grafana for metrics
* Netdata for live system stats
* Pi-hole for network-wide ad blocking
