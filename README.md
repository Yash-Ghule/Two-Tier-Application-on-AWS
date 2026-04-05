# 🚀 Two-Tier Application Deployment on AWS

## 📌 Overview

This project demonstrates the deployment of a **two-tier web application** on AWS with proper networking, security, and end-to-end integration.

The architecture separates:

* **Frontend Layer** – User Interface (React)
* **Backend Layer** – REST API (Flask)

The application is deployed on AWS using EC2 instances and follows basic production-oriented practices for deployment and communication between services.

---

## 🏗️ Architecture

```
User → Frontend (React) → Backend (Flask API)
```

### Key Components:

* **Frontend:** ReactJS application served on EC2
* **Backend:** Python Flask REST API
* **Infrastructure:** AWS EC2 instances within the same VPC

---

## ☁️ AWS Infrastructure

### EC2 Instances:

* Frontend Server (Ubuntu)
* Backend Server (Ubuntu)

### Networking:

* Both instances deployed within the same **VPC**
* Communication enabled via public endpoints

### Security Groups:

* **Frontend SG:**

  * HTTP (80) → Open to internet (0.0.0.0/0)
  * SSH (22) → Restricted to personal IP

* **Backend SG:**

  * API Port (5000) → Open
  * SSH (22) → Restricted to personal IP

---

## ⚙️ Deployment Steps

### 1. Infrastructure Setup

* Launched two EC2 instances (frontend & backend)
* Configured security groups for controlled access
* Ensured both instances are in the same VPC

---

### 2. Backend Deployment

* Connected to backend EC2 via SSH
* Installed dependencies:

  * Python3, pip, virtualenv, git
* Cloned repository and installed requirements
* Started Flask application

Backend runs on:

```
http://<BACKEND_PUBLIC_IP>:5000
```

---

### 3. Frontend Deployment

* Connected to frontend EC2 via SSH
* Installed Node.js, npm, and git
* Cloned frontend repository
* Updated configuration with backend API URL:

```json
{
  "backendUrl": "http://<BACKEND_PUBLIC_IP>:5000"
}
```

* Built and served React application on port 80

---

### 4. Integration & Validation

* Accessed frontend via browser
* Triggered API calls from frontend
* Verified successful backend responses
* Confirmed end-to-end functionality

---

## 🐞 Issues Encountered & Fixes

### 1. Backend Not Reachable Initially

**Cause:**

* Flask app was bound to `127.0.0.1` (localhost only)

**Fix:**

* Updated binding to `0.0.0.0`
* Enabled external access via EC2 public IP

---

### 2. Frontend Failing After Backend Fix

**Cause:**

* React app uses build-time configuration
* Backend URL was incorrectly set during build

**Fix:**

* Updated `config.json` with correct backend IP
* Rebuilt frontend application
* Cleared browser cache

---

### 3. Backend Private IP Not Accessible from Browser

**Cause:**

* Browser runs on user's machine, not inside VPC
* Private IPs are not accessible externally

**Key Insight:**

* Frontend must call backend using **public endpoint or proxy**

---

## 🔐 Security & Networking Learnings

* Importance of **correct service binding (0.0.0.0 vs localhost)**
* Role of **security groups in access control**
* Understanding **public vs private network access**
* Realization that frontend runs in the **user's browser, not EC2**

---

## 🧠 Key Learnings

* Hands-on experience with **AWS EC2 provisioning**
* Understanding of **two-tier architecture deployment**
* Practical exposure to **frontend-backend integration**
* Debugging real-world **networking and deployment issues**
* Importance of **configuration management in frontend builds**

---

## 📌 Future Improvements

* Use **Nginx as reverse proxy**
* Containerize application using **Docker**
* Deploy using **Kubernetes**
* Add **CI/CD pipeline**
* Improve backend security (restrict API access)

---

## 🏁 Conclusion

This project demonstrates the foundational concepts of:

* Cloud deployment
* Service communication
* Networking and security
* Debugging real-world issues

It serves as a base for more advanced architectures like **three-tier systems and containerized deployments**.
