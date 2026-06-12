# SAMY DevOps Engineer Case Study

This project demonstrates the deployment of a Kubernetes-based web application using Infrastructure as Code, monitoring and automation.

Components:

- Terraform
- Kind Kubernetes
- Nginx
- ConfigMap
- Prometheus
- Grafana
- Ansible

---

## Repository Structure

```text
samy-devops-case-study/

README.md

docs/
└── architecture.png

terraform/
├── main.tf
├── providers.tf
└── versions.tf

k8s/
├── configmap.yaml
├── deployment.yaml
└── service.yaml

ansible/
└── site.yml

screenshots/
├── terraform-apply.png
├── kubectl-get-nodes.png
├── kubectl-get-pods.png
├── kubectl-get-svc.png
├── prometheus-targets.png
└── grafana-dashboard.png
```

---

## Architecture

![Architecture](docs/architecture.png)

---

## Design Decisions

### Terraform

Terraform is used to provision a local Kind Kubernetes cluster.

Kind was selected because it provides a lightweight Kubernetes environment suitable for local deployment and rapid testing.

### Kubernetes

The application is deployed using:

- ConfigMap: provides application configuration.
- Deployment (2 replicas): ensures application availability through multiple replicas.
- ClusterIP Service: provides stable internal networking.

### Monitoring

Prometheus collects metrics from Kubernetes components and application pods.

Grafana visualizes:

- CPU usage
- Memory usage
- Pod health
- Uptime

### Automation

Ansible automates:

- Terraform deployment
- Kubernetes resource deployment
- Monitoring stack installation

This improves repeatability and reduces manual effort.

--- 

## Deployment

### Terraform

```bash
terraform init
terraform apply
```

### Kubernetes

```bash
kubectl apply -f k8s/
```

### Monitoring

```bash
helm install monitoring prometheus-community/kube-prometheus-stack
```

### Automation

```bash
ansible-playbook site.yml
```

---

## Production Improvements

For a production environment I would:

- Replace Kind with EKS
- Implement CI/CD pipelines
- Add TLS certificates
- Use external secrets management
- Configure alerting
- Implement high availability
- Add persistent storage
