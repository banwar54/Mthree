# **Kubernetes Core Concepts**
- **Pods**: The smallest deployable unit in Kubernetes, running our Flask application.
- **Deployments**: Manages rolling updates and ensures multiple replicas are running.
- **Services**: Exposes the application using **NodePort** and **Port Forwarding**.
- **ConfigMaps & Secrets**: Stores environment variables and sensitive credentials securely.
- **Persistent Volumes & Claims**: Provides persistent storage for the application.
- **Horizontal Pod Autoscaler (HPA)**: Scales pods dynamically based on CPU and memory usage.
- **Namespaces**: Organizes and isolates resources (created `k8s-demo` namespace).
- **Kubernetes Dashboard**: Web-based UI for managing the cluster.
- **Validation Disabled Deployment**: Used `--validate=false` to bypass API schema validation issues.
- **Minikube Reset & Connectivity Fixes**: Used `minikube-reset-script.sh` to resolve WSL2-related networking issues.

### **Docker & Containerization**
- **Dockerfile**: Defines how to build the Flask application container image.
- **Building Docker Images**: `docker build -t k8s-master-app:latest .`
- **Using Minikube’s Docker Daemon**: Ensured images were built inside Minikube to avoid external registry pushes.

### **Networking & Accessing the App**
- **Port Forwarding**: Used `kubectl port-forward` with retries to expose the app.
- **NodePort**: Retrieved Minikube IP using `minikube ip` and accessed via `30080`.
- **Service Discovery**: Used `minikube service k8s-master-app -n k8s-demo`.
- **Port Handling & Collision Avoidance**: If `8080` was in use, script auto-switched ports.
- **WSL2 Network Fixes**: Reset `wsl.conf` and DNS settings for stable connectivity.

---
# **Kubernetes Deployment Guide**

## **Explanation of the k8s.sh Script**
The provided `k8s.sh` script is a comprehensive Kubernetes deployment automation script that simplifies the process of deploying a containerized application using Kubernetes.

### **Key Features of the Script**

#### **Project Setup**
- Creates a structured directory layout (`k8s-master-app`) with subfolders for application files, Kubernetes manifests, configuration files, logs, and scripts.
- Generates essential Kubernetes YAML configuration files dynamically.

#### **Application Setup**
- Defines a Flask-based Python application (`app.py`).
- Provides a `Dockerfile` to containerize the application.
- Defines the necessary dependencies in `requirements.txt`.

#### **Kubernetes Resources**
- **Namespaces**: Defines `k8s-demo` as an isolated environment.
- **ConfigMaps & Secrets**: Manages application configuration and sensitive credentials.
- **Deployments**: Manages replicas of the application pods.
- **Services**: Exposes the application via **NodePort** for external access.
- **Auto-scaling (HPA)**: Enables automatic pod scaling based on CPU/memory usage.


---

## **Running the Minikube Reset Script**
```bash
chmod +x minikube-reset-script.sh
./minikube-reset-script.sh
```
**Actions Taken:**
- Stopped & deleted any existing Minikube clusters using `minikube delete --all --purge`.
- Fixed WSL2 networking issues by updating `/etc/wsl.conf` and setting Google DNS (`8.8.8.8`).
- Restarted Minikube with optimized settings using `minikube start --driver=docker ...`.
- Verified Kubernetes API connectivity using `kubectl get nodes`.

## **Running the Deployment Script**
```bash
chmod +x deploy-no-validate.sh
./deploy-no-validate.sh
```
**Actions Taken:**
- Checked for required dependencies (`kubectl`, `docker`, `minikube`).
- Verified if Minikube was running using `minikube status`.
- Configured Docker to use Minikube’s Docker daemon (`eval $(minikube docker-env)`).


## **Checking Deployment Status**
```bash
kubectl -n k8s-demo get deployments --timeout=10s
kubectl -n k8s-demo get pods --timeout=10s
```
**Actions Taken:**
- Displayed **deployment and pod status** instead of blocking execution indefinitely.


## **Accessing the Application**
### **Option 1: Port Forwarding (Localhost)**
```bash
kubectl -n k8s-demo port-forward svc/k8s-master-app 8080:80
```
Opened: `http://localhost:8080`

### **Option 2: NodePort (Minikube IP)**
```bash
minikube ip  # Get the Minikube IP
```
Accessed at: `http://<MINIKUBE-IP>:30080`

## **Opening the Kubernetes Dashboard**
```bash
minikube dashboard
```
Opened the web-based UI for monitoring and managing the Kubernetes cluster.

## **Cleaning Up Deployment**
```bash
./scripts/cleanup.sh
```
**Actions Taken:**
- Deleted all Kubernetes resources (pods, services, deployments, etc.).
- Stopped Minikube if no longer needed.


# **Key Concepts Covered**
- **Kubernetes Components**: Pods, Deployments, Services, ConfigMaps, Secrets, Persistent Volumes, and Horizontal Pod Autoscaler (HPA).
- **Minikube Setup & Reset**: Resolving WSL2 networking issues and optimizing the cluster.
- **Docker Image Build**: Using Minikube’s Docker daemon and retry logic for reliable builds.
- **Deployment Automation**: Applying Kubernetes manifests with `--validate=false` to bypass schema validation issues.
- **Application Accessibility**: Port forwarding, NodePort access, and Kubernetes Dashboard usage.
- **Cleanup & Resource Management**: Deleting all Kubernetes resources and stopping Minikube when needed.

# **Execution Summary**
1. **Minikube Reset**: Stopped existing clusters, fixed WSL2 networking issues, and restarted Minikube.
2. **Deployment Script Execution**: Verified dependencies, set up Minikube, and configured Docker.
3. **Docker Image Build**: Ensured connectivity and retried failed builds.
4. **Kubernetes Resource Deployment**: Created namespaces, ConfigMaps, Secrets, Persistent Volumes, Deployments, and Services.
5. **Status Verification**: Checked pod and deployment statuses.
6. **Application Exposure**: Used port forwarding and NodePort to access the application.
7. **Monitoring**: Opened the Kubernetes Dashboard.
8. **Cleanup**: Deleted resources and stopped Minikube when no longer needed.