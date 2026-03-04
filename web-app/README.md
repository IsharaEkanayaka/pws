Provides a lightweight, intent-driven web interface to automate infrastructure-as-code on Proxmox VE. Instead of manual CLI execution or static CI/CD pushes, developers can describe their cluster needs (e.g., number of workers) via a web UI, which then orchestrates the Packer → Terraform pipeline.

# Local Setup & Testing
## 1. Prerequisites
-**Python 3.10+**

-**Terraform installed locally.**

-**SSH Tunnel (if working outside the university network):**

```bash
ssh -L 8006:10.40.19.230:8006 <e-number>@tesla.ce.pdn.ac.lk
```
## 2.Configure Credentials
Create a terraform/terraform.tfvars file (this is gitignored):

```powershell
Terraform
proxmox_api_url          = "https://localhost:8006/api2/json"
proxmox_api_token_id     = "YOUR_TOKEN_ID"
proxmox_api_token_secret = "YOUR_TOKEN_SECRET"
```
## 3. Run the Web App

```powershell
cd web-app
python3 -m venv venv
source venv/bin/activate  # On Windows use: venv\Scripts\activate
pip install flask
python app.py
```
Access the UI at http://localhost:5000


# Architecture Detail

- **Flask (Web-App)**  
  Captures user intent and triggers shell commands.

- **Terraform**  
  Manages the VM lifecycle and resource allocation.

- **Packer**  
  Creates the base Ubuntu Server 22.04 templates.

