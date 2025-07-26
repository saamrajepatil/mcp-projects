
### Project: AWS Architecture Diagrams with Amazon Q CLI & MCP 

#### Overview

This guide shows how to install **Amazon Q CLI** on Linux, set up **MCP servers**, and use them to generate AWS architecture diagrams from natural-language prompts. MCP enables Amazon Q to access context (e.g., AWS icons, documentation, and drawing logic) via lightweight plugin servers, significantly enhancing diagram generation capabilities.

---

### 🔧 What Is MCP?

* **MCP** stands for **Model Context Protocol**, a standardized interface that allows external tools (MCP servers) to provide context-aware data and logic to AI agents like Amazon Q CLI.
* Example MCP servers include AWS Diagram MCP (for generating visuals) and Documentation MCP (for fetching AWS best practices).

* <img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/146f5e9f-0e82-4bd0-a2ef-0a262f95e174" />


---

### 🧪 Linux Setup (Ubuntu )

```bash
# 1. Update packages
sudo apt update -y
sudo apt install -y libfuse2 graphviz

# 2. Download and install Amazon Q CLI
wget https://desktop-release.q.us-east-1.amazonaws.com/latest/amazon-q.deb
sudo apt install -y ./amazon-q.deb

# 3. Login
q login
# Choose "Use for Free with Builder ID" and follow browser verification

# 4. Verify installation
q --version
```

---

### 🧠 Configure MCP Server

Create MCP configuration file at `~/.aws/amazonq/mcp.json`:

```json
{
  "mcpServers": {
    "awslabs.aws-diagram-mcp-server": {
      "command": "uvx",
      "args": ["awslabs.aws-diagram-mcp-server"],
      "env": {"FASTMCP_LOG_LEVEL": "ERROR"},
      "autoApprove": [],
      "disabled": false
    },
    "awslabs.aws-documentation-mcp-server": {
      "command": "uvx",
      "args": ["awslabs.aws-documentation-mcp-server@latest"],
      "env": {"FASTMCP_LOG_LEVEL": "ERROR"},
      "autoApprove": [],
      "disabled": false
    }
  }
}
```
Linux / WSL
sudo snap install astral-uv --classic

---

### 🚀 Workflow: Generate AWS Diagram

1. Launch Amazon Q chat:

   ```bash
   q chat
   ```
2. Use prompts such as:

   ```
   Create a diagram for a multi-AZ web application with ALB, EC2 ASG, and RDS.  
   Check AWS best practices via documentation before generating.
   ```
3. Amazon Q will:

   * Fetch AWS docs using Documentation MCP tool
   * Generate Python code with the Diagram MCP server
   * Render an architecture diagram (e.g., PNG/SVG)
   * Save it to `~/.aws/amazonq/generated-diagrams/`

---

### 🗂️ Example Architecture Prompt & Output

**Prompt:**

> Diagram a three‑tier architecture: ALB → EC2 AutoScaling Group over two AZs → RDS. Include VPC, public/private subnets, IGW, security groups, and Route 53.

**MCP Flow:**

* Documentation MCP pulls relevant AWS guidance
* Diagram MCP maps icon set & networking layout
* Generates a diagram showing ALB, EC2 ASG, RDS, subnet clusters, security groups

---

### 🧭 Architecture Diagram Flow (Text Representation)

```
User prompt → Amazon Q CLI → MCP Documentation tool → Best-practice validation  
        ↓  
   AWS Diagram MCP → Produces Python + diagrams code → Renders Image → Saved locally
```

---

Please find the migration zantac migration project architecture digram i created with amazon q and mcp setup.

<img width="3053" height="6949" alt="cloud-migration-architecture" src="https://github.com/user-attachments/assets/cb4c30e9-627e-4ab3-9d38-4bc27143c586" />


### ✅ Benefits

* No need for manual Visio/drawing tools
* Diagrams adhere to AWS best practices automatically
* Iterative diagram revision via prompt refinement (e.g. changing services or layout).

