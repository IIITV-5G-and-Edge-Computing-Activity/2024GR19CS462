---

## 🚀 DevOps Setup for SplitWise Clone Project

This guide will walk you through the *entire DevOps setup process* for running the SplitWise project using *VS Code, Node.js, Jenkins, Docker, Kubernetes (Minikube), MongoDB, Apache Kafka, Valkey (Redis Alternative), and Aiven Cloud Services*.

---

## 📁 Prerequisites

Make sure you have the following:

•⁠  ⁠A computer with *Linux OS* (for server setup)
•⁠  ⁠Internet connection
•⁠  ⁠Basic understanding of DevOps tools
•⁠  ⁠An Aiven.io account (free trial available)

---

## 🛠️ Step-by-Step Setup Instructions

### 1. Install Visual Studio Code (VS Code)

Install VS Code from the [official website](https://code.visualstudio.com/).

---

### 2. Clone the SplitWise Repository

⁠ bash
git clone https://github.com/tanuj-saini/SplitWise.git
cd SplitWise
npm install
 ⁠

---

### 3. Install Node.js (v20.6.1)

Download Node.js v20.6.1 from [official Node.js site](https://nodejs.org/download/release/v20.6.1/) and install it.

Verify installation:

⁠ bash
node -v
npm -v
 ⁠

---

### 4. Install Jenkins (Latest Version)

Follow the [official Jenkins installation guide](https://www.jenkins.io/doc/book/installing/) for your OS.

Start Jenkins:

⁠ bash
sudo systemctl start jenkins
 ⁠

Access it via: ⁠ http://localhost:8080 ⁠

---

### 5. Set Up MongoDB

Follow [MongoDB installation guide](https://www.mongodb.com/docs/manual/installation/).

After installation:

⁠ bash
sudo systemctl start mongod
 ⁠

Update ⁠ .env ⁠ file:

⁠ env
MONGODB_URI=mongodb://localhost:27017/your-database-name
PORT=7070
 ⁠

---

### 6. Create an Aiven Account

Visit: https://aiven.io and create an account.

---

### 7. Setup Apache Kafka on Aiven

•⁠  ⁠Spin up *Kafka service*
•⁠  ⁠After creation, collect the following keys:
  - ⁠ KAFKA_SSL_CA_PATH ⁠
  - ⁠ KAFKA_SASL_PASSWORD ⁠
  - ⁠ KAFKA_SASL_USERNAME ⁠
  - ⁠ KAFKA_BROK ⁠

🔐 Download Kafka CA Certificate:
•⁠  ⁠Rename it as ⁠ ca.cer ⁠
•⁠  ⁠Place it in the *root directory* of the cloned repo

---

### 8. Setup Valkey (Redis) on Aiven

•⁠  ⁠Spin up *Valkey service*
•⁠  ⁠After creation, collect the following keys:
  - ⁠ REDIS_HOST ⁠
  - ⁠ REDIS_PORT ⁠
  - ⁠ REDIS_USERNAME ⁠
  - ⁠ REDIS_PASSWORD ⁠

---

### 9. Final ⁠ .env ⁠ Configuration

Update your ⁠ .env ⁠ file with all collected values:

---

### 10. Copy ENV Variables to Kubernetes Config

Copy the above variables into the Kubernetes config file at:

⁠ bash
kubernetes/app-configmap.yaml
 ⁠

---

### 11. Setup Jenkins Pipeline

•⁠  ⁠Start Jenkins at: ⁠ http://localhost:8080 ⁠
•⁠  ⁠Create a *New Project* > Select *Pipeline*
•⁠  ⁠Go to the *Pipeline section*
•⁠  ⁠Paste the contents of the ⁠ Jenkinsfile ⁠ from the cloned repo

---

### 12. Skip This Section if Using AWS or Any Cloud Server

### 13. Server Setup (for Local Linux Device)

Ensure your Linux device has:

•⁠  ⁠Docker
•⁠  ⁠Minikube (Kubernetes)
•⁠  ⁠Ansible
•⁠  ⁠Node.js

Install SSH Server on *Server Device*:

⁠ bash
sudo apt update
sudo apt-get install openssh-server
 ⁠

Get ⁠ username ⁠ and ⁠ ip ⁠ from *Server Device*:

⁠ bash
whoami
ip a
 ⁠

Now from *Client Device*:

⁠ bash
ssh username@ip
 ⁠

Make sure both devices are connected to the *same network*.

---

### 14. Setup Jenkins SSH Connection

#### A. Install SSH Agent Plugin

•⁠  ⁠Go to Jenkins Dashboard > Manage Jenkins > Manage Plugins > Install *SSH Agent*

#### B. Add SSH Key

•⁠  ⁠Go to: *Manage Jenkins* > *Credentials* > Global
•⁠  ⁠Add a new credential:
  - Kind: *SSH Username with private key*
  - Enter your server's SSH *username*
  - Choose *Enter directly* and paste the *private RSA key* of the server

#### C. Reference in Jenkinsfile

•⁠  ⁠Go to Pipeline > *Pipeline Syntax*
•⁠  ⁠Select Sample Step: ⁠ sshagent: SSH Agent ⁠
•⁠  ⁠Use the ID of the SSH credential you created
•⁠  ⁠Replace:
  - ⁠ ssh username@ip ⁠ with your real values
  - Any path with your real paths
•⁠  ⁠Replace Docker push stage with your *DockerHub credentials*

---

### 15. Build and Deploy

#### A. Connect to Server Terminal (from client):

⁠ bash
ssh username@ip
 ⁠

#### B. Start Minikube:

⁠ bash
minikube start
 ⁠

#### C. Trigger Jenkins Build

•⁠  ⁠Go to Jenkins Dashboard > Your Pipeline
•⁠  ⁠Click on *Build Now*

---

### 16. Access Services

Once build completes successfully:

⁠ bash
kubectl get services
 ⁠

You will see ports for:

•⁠  ⁠Grafana
•⁠  ⁠Kubernetes Dashboard
•⁠  ⁠Prometheus Server
•⁠  ⁠SplitWise

You can access these using *port forwarding* or directly via the assigned NodePort.

---

## ✅ Project Live!

This setup enables a fully functional DevOps environment with CI/CD pipelines, Kafka & Redis integration, container orchestration, and cloud infrastructure—all built around the SplitWise clone app.

---

## 🙌 Author

Developed with ♥️ by Tanuj Saini  
Guide written by: 2024GR19CS462

---
