Simple App – Helm Chart
This Helm chart deploys the Simple App, a lightweight Node.js application exposed on port 3000. It includes Kubernetes Deployment, Service, Ingress (if you wan to expose apllication using specified hosts), ServiceMonitor (only if prometheus operator is installed in the cluster), and HPA configurations.

⸻

Features
•	Deploys a Node.js web application
•	Configurable replica count
•	Exposes application on port 3000
•	Supports:
•	Kubernetes Service (ClusterIP)
•	Ingress (Nginx, optional)
•	Horizontal Pod Autoscaler (optional)
•	ServiceMonitor for Prometheus (optional)
•	Custom environment variables
•	Fully customizable using values.yaml
Chart Structure
simple-app/ ├── Chart.yaml ├── README.md ├── values.yaml └── templates/ ├── deployment.yaml ├── service.yaml ├── ingress.yaml ├── hpa.yaml ├── serviceaccount.yaml ├── servicemonitor.yaml ├── ecr-secret.yaml ├── pdb.yaml ├── NOTES.txt ├── _helpers.tpl

Installation
Add the chart folder or registry source, then run: helm install simple-app ./simple-app

Upgrade helm upgrade simple-app ./simple-app

Uninstall helm uninstall simple-app

Configuration (values.yaml) Below are the most important parameters.

Application Settings
Key Description Default image.repository Docker image name your-docker-repo/simple-app image.tag Image tag latest replicaCount Number of pod replicas 1 containerPort App port 3000

Service
Key Description Default service.type Kubernetes Service type ClusterIP service.port External service port 3000

Ingress
Key Description ingress.enabled Enable ingress ingress.className Ingress class (nginx) ingress.hosts Domain for application

Example ingress: enabled: true className: nginx hosts: - host: nodeapp.68.233.108.177.nip.io path: /

ServiceMonitor (optional)

Enable if Prometheus Operator is installed: serviceMonitor: enabled: true interval: 30s

Testing the Deployment

After installation: kubectl get pods -l app=simple-app

Port-forward to access locally: kubectl port-forward svc/simple-app 3000:3000

Visit: http://localhost:3000

Notes: To view post-install information: helm status simple-app

If README packaging is enabled: helm show readme simple-app

Contributing Feel free to submit PRs or issues to improve the chart.
