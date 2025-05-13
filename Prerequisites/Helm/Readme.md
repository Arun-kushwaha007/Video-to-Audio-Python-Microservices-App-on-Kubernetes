# 🧭 Helm: Kubernetes Package Manager (Zero to Hero Guide)

## 📌 What is Helm?

**Helm** is the **package manager for Kubernetes**. It helps you define, install, and upgrade complex Kubernetes applications using reusable templates called **charts**.

---

## 📦 Key Concepts

| Term       | Description                                                |
|------------|------------------------------------------------------------|
| Chart      | A Helm package containing Kubernetes resource templates    |
| Values     | Configuration data used by templates                       |
| Template   | YAML files using Go templates to render K8s manifests      |
| Release    | An instance of a chart running in your cluster             |

---

## 🛠️ Why Use Helm?

- 🧩 Simplifies multi-resource Kubernetes deployments
- 🔁 Reusable, versioned, parameterized configs
- 💡 Easy upgrades and rollbacks
- 🤖 CI/CD and GitOps friendly

---

## 📥 Installation

### ✅ Install Helm CLI

**Linux/macOS**:
---
 
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 |  
---

**Windows (via Chocolatey)**:

choco install kubernetes-helm


**Verify Installation**:
helm version


### 🚀 Using Helm
## 1. Add a Chart Repository
 
helm repo add bitnami https://charts.bitnami.com/bitnami

## 2. Search for Charts
 
helm search repo wordpress

## 3. Install a Chart
 
helm install my-wordpress bitnami/wordpress

## 4. List Releases

helm list

## 5. Uninstall a Release
 
helm uninstall my-wordpress

## 🧰 Create Your Own Helm Chart
 
helm create mychart
cd mychart

# Chart Directory Structure
 
 
mychart/
├── Chart.yaml        # Metadata
├── values.yaml       # Configurable values
├── charts/           # Dependent charts
├── templates/        # Kubernetes manifests with Go templating
│   ├── deployment.yaml
│   ├── service.yaml
│   └── _helpers.tpl


# 📑 Sample values.yaml
 
appName: myapp
replicaCount: 2
image:
  repository: nginx
  tag: latest

# 🧠 Template Example (deployment.yaml)

apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ .Values.appName }}
spec:
  replicas: {{ .Values.replicaCount }}
  selector:
    matchLabels:
      app: {{ .Values.appName }}
  template:
    metadata:
      labels:
        app: {{ .Values.appName }}
    spec:
      containers:
        - name: {{ .Values.appName }}
          image: "{{ .Values.image.repository }}:{{ .Values.image.tag }}"

# 🎛️ Overriding Values
Inline:
 
 
helm install myapp ./mychart --set replicaCount=3,image.tag=stable

With a file:

helm install myapp ./mychart -f myvalues.yaml

# 🔁 Helm Lifecycle Commands
 
helm install <release> <chart>
helm upgrade <release> <chart>
helm rollback <release> <revision>
helm uninstall <release>
helm list
helm history <release>


# 🧪 Advanced Helm Features
🔹 Templating Functions

Use Go templating syntax:

 
{{ include "mychart.fullname" . }}
{{ default "nginx" .Values.image.repository }}


🔹 Subcharts & Dependencies

In Chart.yaml:
 
 
dependencies:
  - name: redis
    version: 17.0.1
    repository: https://charts.bitnami.com/bitnami
Then:
 
helm dependency update

# 🔹 Hooks

Run jobs during lifecycle events (pre-install, post-upgrade, etc.):
 
annotations:
  "helm.sh/hook": pre-install

# 🔹 Tests

Add test pods in templates/ with:
 
annotations:
  "helm.sh/hook": test

# Run tests: 
 
helm test <release>

# 🌐 Host Your Own Helm Repo
 
helm package mychart
helm repo index .

Host it on GitHub Pages, S3, or any static server.

## 🚀 Popular Charts on ArtifactHub

✅ NGINX Ingress

📊 Prometheus + Grafana

🔐 Keycloak

🐘 PostgreSQL / MySQL

⚙️ Jenkins

🛰️ ArgoCD

## 🧭 Best Practices

Use separate values.yaml for each environment

Create reusable templates with _helpers.tpl

Use semantic versioning

Always lint your charts:

 **bash**

helm lint mychart

## 📚 Resources

🌐 Official Docs: https://helm.sh/docs/

🔍 Search Charts: https://artifacthub.io/

🧪 Playground: https://helm.sh/helm-demo

📹 YouTube: Bret Fisher, TechWorld with Nana

🔒 Best Practices: https://helm.sh/docs/chart_best_practices/

## 🏁 Summary

**Feature**	          **Purpose**
  Charts	            Package Kubernetes resources
  Templates	            Dynamic YAML files
  values.yaml         	Configuration for templates
  helm install	        Deploy an app
  helm upgrade	        Update the app
  helm rollback	        Roll back to a previous version
  helm repo	            Manage remote charts
  helm create	        Bootstrap a new chart

