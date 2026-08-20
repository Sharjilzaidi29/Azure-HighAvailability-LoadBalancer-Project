# High-Availability Web Infrastructure Deployment using Azure Public Load Balancer

An end-to-end Azure Cloud & DevOps project implementing a highly available, fault-tolerant web infrastructure for **Rand Enterprises Corporation** using Azure Public Load Balancer, Virtual Machines, IIS Web Servers, and Microsoft Entra ID (RBAC).

---

## 📌 Project Overview
The primary objective of this project is to deploy a web application in a highly available environment to ensure zero downtime for end-users. The infrastructure distributes incoming network traffic across multiple healthy virtual machine instances in a backend pool.

To enhance security:
- Virtual Machines housing the application are **not directly exposed** to the public internet (Public IPs are detached).
- All incoming HTTP traffic is routed exclusively through the **Azure Public Load Balancer**.
- **Health Probes** continuously monitor server health, redirecting traffic only to operational instances.
- **Role-Based Access Control (RBAC)** via **Microsoft Entra ID** enforces the principle of least privilege for the Operations Team.

---

## 🏗️ Architecture & Workflow

```text
               [ Internet / Public Traffic ]
                             │
                             ▼
              [ Azure Public Load Balancer ]
                    (VIP:80 / Frontend)
                             │
           ┌─────────────────┴─────────────────┐
           │ (Health Probe: TCP Port 80)       │
           ▼                                   ▼
    [ Webserver1 ]                      [ Webserver2 ]
 (IIS Web Server - VM1)              (IIS Web Server - VM2)
   [ Backend Pool ]                    [ Backend Pool ]
