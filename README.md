# EC2 Monitoring with Grafana, Prometheus

Monitor your EC2 server (or any Linux server) using Prometheus and Grafana, all deployed via Docker Compose.

![Github Actions (1)](https://github.com/user-attachments/assets/a7ec4b90-c9cf-4009-9fa7-b128a67aa52a)

---

## 🚀 Tech Stack

- **Prometheus** – Scrapes metrics from Node Exporter
- **Grafana** – Visualizes metrics on dashboards
- **Node Exporter** – Exposes system metrics on EC2
- **Docker Compose** – Manages Prometheus & Grafana stack

---

---

## 📁 Folder Structure

```
.
├── build-process/docker-compose.yml                # Stack definition
├── monitoring/prometheus.yml                    # Prometheus config file
└── README.md
```

---

## ⚙️ Setup Instructions

### 1. 🚀 Launch Node Exporter on EC2
SSH into the EC2 server and run:

#### Necessary Packages Installation on AWS EC2
Install these Packages

```
# Updates the package index to ensure you have the latest information about #available packages.
sudo apt-get update -y

# Installs the Nginx web server with a confirmation flag (-y) to bypass the prompt.
sudo apt install nginx -y

# Installs Docker from the default Ubuntu package repository.
sudo apt install docker.io -y

# Adds the 'ubuntu' user to the 'docker' group, allowing the user to run Docker #commands without sudo.
sudo usermod -aG docker ubuntu

# Activates the changes made to the user group without requiring a system reboot.
newgrp docker

# Sets read, write, and execute permissions for all users on the Docker socket file 
sudo chmod 777 /var/run/docker.sock

# Downloads the latest version of Docker Compose and saves it to #/usr/local/bin/docker-compose.

sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose


# Makes the Docker Compose binary executable.
sudo chmod +x /usr/local/bin/docker-compose

# Verifies the installation of Docker Compose by displaying its version.
docker-compose --version 

```



---

### 2. 📦 Deploy Monitoring Stack

```bash
git clone https://github.com/codewithmuh/ec2-monitoring-with-grafana-prometheus.git
cd ec2-monitoring-with-grafana-prometheus
sudo docker-compose -f "./build-process/docker-compose.yml" up -d --build
```

---


### 4. 📊 Access Grafana

- URL: `http://YOUR_SERVER_IP:3000`
- Default login: `admin / admin`
- Import Dashboard ID: `1860` (Node Exporter Full)

---


## 📬 Contributing

Pull requests are welcome. For major changes, open an issue first to discuss what you would like to change.

---

## 📝 License

[MIT](LICENSE)

---
