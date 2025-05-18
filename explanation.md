# Explanation of Implementation Choices

## 1. Choice of Kubernetes Objects Used for Deployment

I used Deployment objects for both the frontend and backend services. Deployments are suitable for stateless applications like my React frontend and Node.js/Express backend, as they provide easy rollout/rollback and automatic scaling.

I didn't use StatefulSets, as my application does not require persistent identities, ordered deployment, or stable storage across pod restarts. No stateful database (like MongoDB) was deployed directly inside the cluster.

## 2. Method Used to Expose Pods to Internet Traffic

I used **LoadBalancer Services** to expose both frontend and backend pods to external traffic. This type of service is appropriate for cloud environments (GKE), as it provisions an external IP address and forwards traffic to the pods internally.

Example:
- Frontend: `http://34.60.73.207:3000/`

## 3. Use-of or Lack-of Persistent Storage

I did not implement persistent storage because:
- My app architecture does not include a database within the cluster.
- MongoDB (if used) would ideally be provisioned using a managed service (e.g., MongoDB Atlas), and accessed remotely.
- The frontend and backend containers do not require data persistence between restarts.

## 4. Git Workflow Used

- All work was done on the `main` branch for simplicity.
- After local testing and verification, files were committed with descriptive messages and pushed to GitHub.
- Docker image tags (`v1.0.0`, `v1.0.1`) reflect iterative development and are referenced in Kubernetes manifests for traceability.

## 5. Application Accessibility and Debugging Measures

The application is successfully running and accessible via:
- Frontend: http://34.60.73.207:3000/
- Backend:  http://34.70.235.102:5000/

Debugging measures taken:
- Inspected logs using `kubectl logs`
- Used `kubectl describe` to understand pod failures
- Rebuilt Docker images with corrected entrypoints and environment fixes

## 6. Good Practices Applied

- **Image naming:** I followed semantic versioning in image tags (`v1.0.0`, `v1.0.1`) for clarity and rollback support.
- **Custom image repo:** Pushed images to Docker Hub under my personal namespace (`22225/brian-yolo-client).
- **Clear folder structure:** YAML manifests organized under `manifests/`.
- **Proper resource limits:** CPU and memory requests/limits were defined to prevent overuse.
- **Environment isolation:** Used cloud-native LoadBalancer and did not hard-code internal service IPs.
