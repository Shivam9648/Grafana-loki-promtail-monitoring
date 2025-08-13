# Grafana-loki-promtail-monitoring
# Overview
This project implements a complete observability and log monitoring solution using Grafana for visualization, Loki for log aggregation, and Promtail for log collection. The setup is deployed on Ubuntu EC2 instances and connected via SSH for remote configuration.

# Objectives
* Centralized logging for multiple servers

* Real-time log visualization and analysis

* Easy-to-use Grafana dashboards

* Fully open-source monitoring stack

# Tech Stack
* Grafana – Dashboard and visualization

* Loki – Log aggregation and storage

* Promtail – Log collection from server files

* Ubuntu EC2 – Deployment environment

* SSH – Secure remote access

<img width="1536" height="1024" alt="ChatGPT Image Aug 13, 2025, 06_00_08 PM" src="https://github.com/user-attachments/assets/d3e28e56-d136-4929-b1b8-15bb9b0eba36" />


# Setup Steps
1. Provision Ubuntu EC2 Servers
Launch AWS EC2 instances (Ubuntu 20.04 or 22.04).

2. Install Grafana on Debian or Ubuntu

sudo apt-get install -y apt-transport-https
sudo apt-get install -y software-properties-common wget
sudo wget -q -O /usr/share/keyrings/grafana.key https://apt.grafana.com/gpg.key

Stable release
echo "deb [signed-by=/usr/share/keyrings/grafana.key] https://apt.grafana.com stable main" | sudo tee -a /etc/apt/sources.list.d/grafana.list

# Update the list of available packages
sudo apt-get update

# Install the latest OSS release:
sudo apt-get install grafana

3. Install and Configure Loki
 
* Download Loki Config


wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/cmd/loki/loki-local-config.yaml -O loki-config.yaml

* Run Loki Docker container

docker run -d --name loki -v $(pwd):/mnt/config -p 3100:3100 grafana/loki:2.8.0 --config.file=/mnt/config/loki-config.yaml

4. Install and Configure Promtail

* Download Promtail Config

wget https://raw.githubusercontent.com/grafana/loki/v2.8.0/clients/cmd/promtail/promtail-docker-config.yaml -O promtail-config.yaml

* Run Promtail Docker container

docker run -d --name promtail -v $(pwd):/mnt/config -v /var/log:/var/log --link loki grafana/promtail:2.8.0 --config.file=/mnt/config/promtail-config.yaml

# Dashboards
* Error Logs Dashboard – Filters and displays only error-level logs

* Real-time Logs View – Streams logs directly in Grafana

* Historical Log Search – Search logs using Loki query language

# Screenshots
Grafana Dashboard Example
<img width="1919" height="1013" alt="Screenshot 2025-08-13 173834" src="https://github.com/user-attachments/assets/fae90cda-bb44-447e-adb3-2f94eb0649a8" />


# Outcomes
* Fully functional observability stack

* Real-time and historical log monitoring

*AWS EC2 deployment using SSH

* Easily extendable for any application logs



