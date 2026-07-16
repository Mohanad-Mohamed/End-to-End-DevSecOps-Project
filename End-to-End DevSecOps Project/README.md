# End-to-End DevSecOps Project

A comprehensive DevSecOps demonstration project that showcases the complete software development lifecycle from source code to secure, monitored Kubernetes deployment on AWS EKS.

## 🚀 Overview

This project implements a modern web application with a full DevSecOps pipeline including continuous integration, container security scanning, code quality analysis, infrastructure as code, and production-grade monitoring. It serves as an educational resource for understanding best practices in secure DevOps workflows.

## ✨ Features

- **Modern Web Application**: Simple Node.js server with responsive HTML/CSS frontend
- **CI/CD Pipeline**: GitLab CI/CD for automated testing and deployment
- **Container Security**: Docker image scanning with Trivy
- **Code Quality**: SonarQube integration for static code analysis
- **Infrastructure as Code**: Terraform for AWS resource provisioning
- **Kubernetes Deployment**: AWS EKS with production-ready configuration
- **Load Balancing**: AWS Load Balancer Controller for traffic distribution
- **Monitoring Stack**: Prometheus and Grafana for metrics and visualization
- **Alerting**: Custom Prometheus rules for application monitoring

## 🛠 Tech Stack

### Application
- **Runtime**: Node.js (>=20)
- **Server**: Native Node.js HTTP server
- **Frontend**: HTML5, CSS3

### DevOps Tools
- **Version Control**: Git
- **CI/CD**: GitLab CI/CD
- **Containerization**: Docker
- **Security Scanning**: Trivy
- **Code Quality**: SonarQube
- **Infrastructure**: Terraform
- **Container Orchestration**: Kubernetes (EKS)
- **Package Manager**: Helm
- **Monitoring**: Prometheus, Grafana
- **Load Balancing**: AWS Load Balancer Controller

### Cloud Platform
- **Provider**: AWS
- **Region**: us-east-1
- **Services**: EKS, EC2, ELB

## 📋 Prerequisites

Before setting up this project, ensure you have:

- Node.js >= 20
- Docker installed
- Git installed
- AWS account with appropriate permissions
- GitLab account
- kubectl installed
- Terraform installed
- Helm installed

## 🏗 Project Structure

```
end-to-end-devops-project/
├── public/
│   ├── index.html          # Main HTML page
│   └── assets/
│       └── styles.css      # Styling
├── src/
│   └── server.js           # Node.js server
├── test/
│   └── server.test.js      # Unit tests
├── terraform/              # Infrastructure as code
├── k8s/                    # Kubernetes manifests
├── .gitlab-ci.yml          # CI/CD pipeline
├── Dockerfile              # Container definition
├── package.json            # Node.js dependencies
└── README.md              # This file
```

## 🚀 Getting Started

### Local Development

1. **Clone the repository**
   ```bash
   git clone https://gitlab.com/devops-project9921421/end-to-end-devops-project.git
   cd end-to-end-devops-project
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Run the application**
   ```bash
   npm start
   ```

4. **Access the application**
   Open your browser and navigate to `http://localhost:3000`

### Running Tests

Execute unit tests with coverage:
```bash
npm test
npm run test:coverage
```

## 🐳 Docker Setup

### Build the Docker Image

```bash
docker build -t end-to-end-devops-project:latest .
```

### Run the Container

```bash
docker run -p 3000:3000 end-to-end-devops-project:latest
```

### Security Scanning with Trivy

Scan the Docker image for vulnerabilities:
```bash
trivy image end-to-end-devops-project:latest
```

## 🔧 CI/CD Pipeline

The GitLab CI/CD pipeline includes the following stages:

1. **Test**: Runs unit tests
2. **Build**: Creates Docker image
3. **Scan**: Scans image with Trivy
4. **Push**: Pushes image to registry
5. **Deploy**: Deploys to Kubernetes

Pipeline configuration is defined in `.gitlab-ci.yml`.

## ☁️ AWS Deployment

### Infrastructure Setup with Terraform

1. **Configure AWS CLI**
   ```bash
   aws configure
   ```

2. **Initialize Terraform**
   ```bash
   cd terraform
   terraform init
   ```

3. **Plan Infrastructure**
   ```bash
   terraform plan
   ```

4. **Apply Infrastructure**
   ```bash
   terraform apply
   ```

### Configure kubectl for EKS

```bash
aws eks update-kubeconfig --name end-to-end-devops-eks --region us-east-1
```

### Verify Cluster Connection

```bash
kubectl get nodes
```

## 🎯 Kubernetes Deployment

### Apply Kubernetes Manifests

```bash
kubectl apply -f k8s/deployment.yaml
kubectl apply -f k8s/service.yaml
kubectl apply -f k8s/ingress.yaml
```

### Verify Deployment

```bash
kubectl get pods -n devops-project
kubectl get svc -n devops-project
kubectl get ingress -n devops-project
```

## 📊 Monitoring Setup

### Install Prometheus and Grafana

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
helm install prometheus prometheus-community/kube-prometheus-stack -n monitoring --create-namespace
```

### Configure Service Monitors

Apply custom ServiceMonitor for application metrics:
```bash
kubectl apply -f k8s/servicemonitor.yaml
```

### Access Grafana

1. Port-forward to Grafana:
   ```bash
   kubectl port-forward svc/prometheus-grafana 3000:80 -n monitoring
   ```

2. Access Grafana at `http://localhost:3000`
   - Default username: `admin`
   - Default password: `prom-operator`

### Configure Prometheus Rules

Apply custom alerting rules:
```bash
kubectl apply -f k8s/prometheus-rules.yaml
```

## 🔍 Monitoring Endpoints

The application exposes the following monitoring endpoints:

- **Health Check**: `http://<application-url>/healthz`
- **Metrics**: `http://<application-url>/metrics` (Prometheus format)

## 🚨 Alerting

The project includes custom Prometheus alerts:

- **WebsiteHighRequestBurst**: Triggers when the website receives more than 20 requests in one minute

View alerts in Prometheus or configure Alertmanager for notifications.

## 📈 Application Metrics

The application tracks the following metrics:

- `devops_project_http_requests_total`: Total HTTP requests by route
- `devops_project_uptime_seconds`: Application uptime in seconds

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request
