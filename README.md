# Amazon DevOps Case Study - CI/CD Pipeline Implementation

[![CI/CD Pipeline](https://img.shields.io/badge/CI/CD-Jenkins-blue)](https://www.jenkins.io)
[![Containerization](https://img.shields.io/badge/Container-Docker-green)](https://www.docker.com)
[![Orchestration](https://img.shields.io/badge/Orchestration-Kubernetes-purple)](https://kubernetes.io)

This repository demonstrates an end-to-end CI/CD pipeline inspired by Amazon's DevOps best practices. It includes containerization, automated deployment, infrastructure as code, and monitoring implementation.

## 🛠️ Tools Used
- **CI/CD Server**: Jenkins
- **Containerization**: Docker
- **Orchestration**: Kubernetes (Minikube/Kind)
- **Infrastructure Automation**: Ansible
- **Monitoring**: Prometheus + Grafana
- **Source Control**: GitHub

## 📦 Prerequisites
- Docker & Docker Compose
- kubectl (Kubernetes CLI)
- Kubernetes cluster (Minikube/Kind recommended)
- Ansible
- Node.js/Python (depending on sample app)
- Jenkins instance
- Prometheus & Grafana (for monitoring)

## 🚀 Getting Started

### 1. Clone Repository
```bash
git clone https://github.com/yourusername/amazon-devops-case-study.git
cd amazon-devops-case-study
```

### 2. Jenkins Setup (Docker)
```bash
cd jenkins
docker-compose up -d
```
Access Jenkins at `http://localhost:8080`

### 3. Build Application Container
```bash
cd app
docker build -t your-dockerhub-username/amazon-devops-app .
```

### 4. Deploy to Kubernetes
```bash
kubectl apply -f kubernetes/
```

## 🔧 Pipeline Configuration

### Jenkins Pipeline Setup
1. Create new pipeline job in Jenkins
2. Set GitHub repository URL
3. Specify Jenkinsfile path: `jenkins/Jenkinsfile`
4. Add credentials:
   - Docker Hub credentials (ID: docker-creds)
   - Kubernetes config file

### GitHub Webhook
1. In GitHub repo settings:
   - Add webhook URL: `http://<JENKINS-IP>:8080/github-webhook/`
   - Content type: application/json

## 📊 Monitoring Setup
```bash
# Deploy Prometheus
kubectl apply -f monitoring/prometheus.yml

# Deploy Grafana
kubectl apply -f monitoring/grafana/
```

Access dashboards:
```bash
kubectl port-forward svc/grafana 3000:3000
```
Open `http://localhost:3000` (default creds: admin/admin)

## 🏃 Running the Pipeline
1. Push changes to GitHub
2. Jenkins automatically triggers:
   - Checkout → Build → Test → Push → Deploy
3. Verify deployment:
```bash
kubectl get pods
kubectl get services
```

## 📂 Project Structure
```
amazon-devops-case-study/
├── docs/                  # Documentation & architecture diagrams
├── app/                   # Application code
│   ├── Dockerfile         # Container configuration
│   └── ...                # App source files
├── kubernetes/            # K8s manifests
│   ├── deployment.yaml    
│   └── service.yaml       
├── jenkins/               # Jenkins configuration
│   ├── Jenkinsfile        
│   └── docker-compose.yml 
├── ansible/               # Infrastructure automation
├── monitoring/            # Observability configs
└── README.md              # This documentation
```

## 🤝 Contributing
1. Fork the project
2. Create your feature branch (`git checkout -b feature/awesome-feature`)
3. Commit changes (`git commit -m 'Add awesome feature'`)
4. Push to branch (`git push origin feature/awesome-feature`)
5. Open a Pull Request

---

**Note**: Replace all `your-dockerhub-username` occurrences with your actual Docker Hub username. Ensure proper security measures for production use (secrets management, RBAC, etc.).
