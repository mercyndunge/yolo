# 🛍️ Yolo E-Commerce App (MERN) – Kubernetes Deployment

This project involves the containerization and Kubernetes deployment of a full-stack Yolo e-commerce application. The application consists of a React frontend, a Node.js/Express backend, and a MongoDB database (external). The backend and frontend are deployed to a GKE Kubernetes cluster using Docker images and YAML manifests.

---

## 🌐 Live App Links

- 🔗 **Frontend**: [http://34.60.73.207:3000](http://34.60.73.207:3000)
- 🔗 **Backend**: [http://34.70.235.102:5000](http://34.70.235.102:5000)

---

## 📦 Technologies Used

- Kubernetes (GKE)
- Docker
- React (Frontend)
- Node.js + Express (Backend)
- MongoDB (via external service)
- LoadBalancer Services

---

## 📁 Project Structure

yolo/
├── manifests/ # Kubernetes YAML files
│ ├── backend-deployment.yaml
│ ├── frontend-deployment.yaml
├── client/ # React frontend
│ └── Dockerfile
├── server/ # Node.js backend
│ └── Dockerfile
├── explanation.md # Justification for K8\ubernetes architecture choices
└── README.md # This file


---

## ⚙️ Kubernetes Architecture Overview

- **Deployments** used for both frontend and backend
- **LoadBalancer Services** expose the apps to external traffic
- **No StatefulSets** used (see [explanation.md](./explanation.md) for reasoning)
- **No persistent storage** implemented (MongoDB hosted externally)

---

## 🐳 Docker Image Tags

| Component | Docker Image | Tag |
|----------|---------------|-----|
| Frontend | `22225/brian-yolo-client` | `v1.0.1` |
| Backend  | `22225/brian-yolo-backend` | `v1.0.0` |

---

## 💡 How to Deploy 

> These are general deployment steps assuming access to a GKE cluster.

1. Clone the repo:
   
   git clone https://github.com/mercyndunge/yolo.git
   cd yolo

2. Apply Kubernetes manifests:

   kubectl apply -f "/home/mercy/Desktop/yolo IP 2/yolo/manifests/frontend-deployment.yaml
   kubectl apply -f "/home/mercy/Desktop/yolo IP 2/yolo/manifests/backend-deployment.yaml

3. Get service external IPs
    
   kubectl get svc

4. Visit the frontend and backend URLs in the browser.


Debugging Measures Taken
Used kubectl logs and kubectl describe to inspect pod failures

Resolved:

CrashLoopBackOff for backend due to missing npm

Incorrect frontend port (5000 instead of 3000)

Webpack OpenSSL error with NODE_OPTIONS=--openssl-legacy-provider

Verified pod readiness and service exposure with:

kubectl get pods
kubectl get svc

