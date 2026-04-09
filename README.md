Project Overview
This repository contains the source code and configuration files required to deploy a scalable Flask backend on Kubernetes. 

File Structure
Layer1_backend.py: The Flask application script.


dockerfile: Instructions for building the Docker image. 

Layer3_deployment.yaml: Kubernetes Deployment configuration.

Layer3_service.yaml: Kubernetes Service configuration for external access.

Technical Specifications
1. Backend API (Layer1_backend.py)
The application is built using the Flask framework and exposes the following routes:

GET /: Automatically redirects the user to the data endpoint.

GET /api/data: Returns a JSON object: {"message": "Hello from the backend!"}.

Host/Port: The app runs on 0.0.0.0 at port 5000.

2. Containerization (dockerfile)
The image is built using the following steps:


Base Image: python:3.10. 


Dependencies: Installs packages listed in requirements.txt. 


Execution: Starts the backend script using the Python interpreter. 

3. Kubernetes Orchestration
The deployment is split into two layers:

Deployment (Layer3_deployment.yaml):

Replicas: Ensures 2 instances (pods) of the application are always running.

Image: Uses dhinesh2001/python-app:v1.

Container Port: Listens on port 5000.

Service (Layer3_service.yaml):

Type: NodePort, allowing access from outside the cluster.

Internal Port: Port 80 within the cluster.

NodePort: Exposed on port 30007 on the host machine.

Target Port: Maps traffic to the container's port 5000.

Deployment Steps
Build the Docker Image:

Bash
docker build -t dhinesh2001/python-app:v1 .
Apply Kubernetes Manifests:

Bash
kubectl apply -f Layer3_deployment.yaml
kubectl apply -f Layer3_service.yaml
Access the Application:
Once deployed, the API will be accessible at http://<Node-IP>:30007/api/data.
