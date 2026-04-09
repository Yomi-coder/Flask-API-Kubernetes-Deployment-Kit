# Flask API Kubernetes Deployment Kit

This project provides a complete template for building, containerizing, and deploying a simple Python Flask backend to a Kubernetes cluster.

## About

A complete three-layer DevOps project demonstrating how to deploy a Python Flask backend application from development to Kubernetes orchestration.

## 📋 Project Overview

This project showcases a full DevOps workflow with three distinct layers:

1. **Layer 1 (Backend)**: Python Flask API application
2. **Layer 2 (Containerization)**: Docker containerization
3. **Layer 3 (Orchestration)**: Kubernetes deployment and service

The application is a simple REST API built with Flask that serves data through HTTP endpoints.

## 🏗️ Architecture

```
Developer Code (Flask API)
        ↓
   Docker Image
        ↓
  Docker Container
        ↓
Kubernetes Deployment
        ↓
     Kubernetes Pods
        ↓
  Kubernetes Service
        ↓
      Users
```

## 📁 File Structure

```
.
├── Layer1_backend.py              # Python Flask backend application
├── dockerfile                     # Docker container configuration
├── Layer3_deployment.yaml         # Kubernetes deployment config
├── Layer3_service.yaml            # Kubernetes service config
├── requirements.txt               # Python dependencies
└── README.md                       # This file
```

## 🚀 Quick Start

### Prerequisites

- Python 3.10+
- Docker
- Kubernetes (kubectl)
- pip (Python package manager)

### Layer 1: Running Locally

1. **Install dependencies**:
   ```bash
   pip install -r requirements.txt
   ```

2. **Run the application**:
   ```bash
   python Layer1_backend.py
   ```

3. **Access the API**:
   - Root endpoint: `http://localhost:5000/`
   - API endpoint: `http://localhost:5000/api/data`

### Layer 2: Docker Containerization

1. **Build the Docker image**:
   ```bash
   docker build -t python-app:v1 .
   ```

2. **Verify the image**:
   ```bash
   docker images
   ```

3. **Run the Docker container**:
   ```bash
   docker run -p 5000:5000 python-app:v1
   ```

### Layer 3: Kubernetes Deployment

1. **Deploy to Kubernetes**:
   ```bash
   kubectl apply -f Layer3_deployment.yaml
   kubectl apply -f Layer3_service.yaml
   ```

2. **Verify the deployment**:
   ```bash
   kubectl get deployments
   kubectl get pods
   kubectl get services
   ```

3. **Access the service**:
   - Find the Node IP: `kubectl get nodes -o wide`
   - Access at: `http://<NODE-IP>:30007/api/data`

## 📡 API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | Root endpoint (redirects to `/api/data`) |
| `/api/data` | GET | Returns a welcome message from the backend |

### Example Response

```json
{
  "message": "Hello from the backend!"
}
```

## 🛠️ Technology Stack

- **Backend Framework**: Flask (Python)
- **Containerization**: Docker
- **Orchestration**: Kubernetes
- **Python Version**: 3.10

## 📝 Configuration Details

### Docker Configuration
- **Base Image**: python:3.10
- **Working Directory**: `/app`
- **Port**: 5000
- **Entry Point**: `Layer1_backend.py`

### Kubernetes Configuration
- **Replicas**: 2 pods
- **Container Port**: 5000
- **Service Type**: NodePort
- **Service Port**: 80
- **Target Port**: 5000
- **Node Port**: 30007

## 🔄 Development Workflow

1. Modify `Layer1_backend.py` for backend changes
2. Update `requirements.txt` if new dependencies are needed
3. Build and test Docker image locally
4. Update Docker image tag and push to registry if needed
5. Apply Kubernetes configurations to deploy changes

## 📚 Learning Resources

- [Flask Documentation](https://flask.palletsprojects.com/)
- [Docker Documentation](https://docs.docker.com/)
- [Kubernetes Documentation](https://kubernetes.io/docs/)

## 📝 Notes

- The application runs on port 5000 by default
- Debug mode is enabled for local development
- The Kubernetes deployment expects the image `username/python-app:v1`
- Update the image name in `Layer3_deployment.yaml` if using a different registry

## 🔗 Additional Resources

For more information, refer to the learning resources and documentation links above.
