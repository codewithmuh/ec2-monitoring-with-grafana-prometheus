# EC2 Monitoring with Grafana, Prometheus & GitHub Actions

Monitor your EC2 server (or any Linux server) using Prometheus and Grafana, all deployed via Docker Compose and automated with GitHub Actions.

![Github Actions (1)](https://github.com/user-attachments/assets/a7ec4b90-c9cf-4009-9fa7-b128a67aa52a)

---

## 🚀 Tech Stack

- **Prometheus** – Scrapes metrics from Node Exporter
- **Grafana** – Visualizes metrics on dashboards
- **Node Exporter** – Exposes system metrics on EC2
- **Docker Compose** – Manages Prometheus & Grafana stack
- **GitHub Actions** – Automates deployment on push

---

## 📌 Architecture

```
                   ┌────────────────────┐
                   │    GitHub Actions  │
                   │ (CI/CD Deployment) │
                   └────────┬───────────┘
                            ▼
                    ┌───────▼────────┐
                    │   Docker Host  │
                    │ (EC2 Instance) │
                    │                │
                    │ ┌────────────┐ │
                    │ │ Prometheus │ │
                    │ └────┬───────┘ │
                    │      ▼         │
                    │  ┌─────────┐   │
                    │  │ Grafana │   │
                    │  └─────────┘   │
                    └──────┬────────┘
                           ▼
               ┌────────────────────┐
               │   EC2 Server       │
               │ (Node Exporter)    │
               └────────────────────┘
```

---

## 📁 Folder Structure

```
.
├── .github/workflows/deploy.yml      # GitHub Actions workflow
├── docker-compose.yml                # Stack definition
├── prometheus.yml                    # Prometheus config file
├── grafana/                          # Grafana provisioning (optional)
└── README.md
```

---

## ⚙️ Setup Instructions

### 1. 🚀 Launch Node Exporter on EC2
SSH into the EC2 server and run:

```bash
docker run -d -p 9100:9100 prom/node-exporter
```

---

### 2. 📦 Deploy Monitoring Stack

```bash
git clone https://github.com/your-username/ec2-monitoring-with-grafana-prometheus.git
cd ec2-monitoring-with-grafana-prometheus
docker-compose up -d
```

---

### 3. 🔧 Configure Prometheus

Ensure your `prometheus.yml` includes:

```yaml
scrape_configs:
  - job_name: 'node_exporter'
    static_configs:
      - targets: ['YOUR_EC2_PUBLIC_IP:9100']
```

---

### 4. 📊 Access Grafana

- URL: `http://YOUR_SERVER_IP:3000`
- Default login: `admin / admin`
- Import Dashboard ID: `1860` (Node Exporter Full)

---

### 5. 🔄 Setup GitHub Actions (CI/CD)

- Add the following secrets in GitHub:
  - `EC2_HOST`
  - `EC2_USER`
  - `EC2_SSH_KEY`

### Sample Workflow (`.github/workflows/deploy.yml`):

```yaml
name: Deploy Monitoring Stack
on:
  push:
    branches: [main]
jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: SSH and Deploy
        uses: appleboy/ssh-action@master
        with:
          host: ${{ secrets.EC2_HOST }}
          username: ${{ secrets.EC2_USER }}
          key: ${{ secrets.EC2_SSH_KEY }}
          script: |
            cd /home/ec2-user/monitoring
            git pull
            docker-compose up -d
```

---

## 📬 Contributing

Pull requests are welcome. For major changes, open an issue first to discuss what you would like to change.

---

## 📝 License

[MIT](LICENSE)

---

## 📸 Screenshots (Optional)

_Add screenshots of Grafana dashboards, Prometheus targets page, etc._

---

