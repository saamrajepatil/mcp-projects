
![Capture](https://github.com/user-attachments/assets/128906d7-4774-4063-99f5-883f20a5ffa3)

## 📦 E-commerce App Deployment on Kubernetes with MCP and Amazon Q

This project showcases the architecture of a typical **E-commerce application** deployed on **Kubernetes** clusters using **MCP Server** and visualized with **Amazon Q CLI**.

---

### 📘 Use Case

* Deploy a cloud-native e-commerce app using Kubernetes.
* Automate and visualize architecture diagrams using [Amazon Q CLI](https://docs.aws.amazon.com/q/cli/).
* Use **MCP protocol** to register microservices and components like frontend, backend, database, and storage into the architecture.

---

### 🧠 What is MCP?

**Model Context Protocol (MCP)** is an open standard for tools like Amazon Q CLI to **query system context models** from running services.

#### ✅ Example MCP Servers:

* `awslabs.aws-diagram-mcp-server`
* `kubernetes-mcp-server`
* `cdk-mcp-server`

---

### 🧩 Components of the E-Commerce App

| Component    | Description                                   |
| ------------ | --------------------------------------------- |
| Frontend     | React or Angular UI hosted in container       |
| Backend      | Node.js/Java microservices on Kubernetes pods |
| Database     | MySQL or MongoDB as a StatefulSet             |
| Object Store | S3-compatible storage (e.g., MinIO)           |
| Gateway      | Ingress or API Gateway in EKS cluster         |

---

### 🖥️ Kubernetes Cluster Setup

* Use EKS or on-premises Kubernetes.
* Deploy microservices using Helm or Kustomize.
* Expose services with Ingress + NGINX controller.
* Monitor via Prometheus + Grafana.

---

### 🛠️ MCP Configuration (`mcp.json`)

```json
{
  "mcpServers": {
    "awslabs.cdk-mcp-server": {
      "command": "uvx",
      "args": ["awslabs.cdk-mcp-server@latest"],
      "env": {
        "FASTMCP_LOG_LEVEL": "ERROR"
      }
    },
    "awslabs.aws-diagram-mcp-server": {
      "command": "uvx",
      "args": ["awslabs.aws-diagram-mcp-server"],
      "env": {
        "FASTMCP_LOG_LEVEL": "ERROR"
      },
      "autoApprove": [],
      "disabled": false
    },
    "kubernetes": {
      "command": "uvx",
      "args": ["kubernetes-mcp-server@latest"],
      "env": {
        "FASTMCP_LOG_LEVEL": "ERROR"
      }
    }
  }
}

```

---

### 🧪 Steps to Generate Architecture Diagram

1. Install [Amazon Q CLI](https://docs.aws.amazon.com/q/cli/latest/userguide/install.html).
2. Configure your `mcp.json`.
3. Run:


<img width="1572" height="538" alt="image" src="https://github.com/user-attachments/assets/7582a668-59b2-4e0f-ac2e-4d98ef1706a8" />

```bash
q describe-architecture --output diagram.png
```



4. View the output diagram (`diagram.png`) showcasing all Kubernetes components auto-discovered via MCP.

---


### 🚀 Tools Used

* 🐳 Docker
* ☸️ Kubernetes / EKS
* 🧩 MCP Server
* 📊 Amazon Q CLI
* 🔐 IAM Roles / Secrets Manager (if applicable)


