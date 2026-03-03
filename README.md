# 🚀 DevOps Internship Task – MEAN Stack CI/CD Deployment

## 📌 Project Overview

In this project, I deployed a full-stack MEAN application using Docker, GitHub Actions, and AWS EC2.
The goal was to containerize the application, automate builds using CI/CD, and expose the app through an Nginx reverse proxy on port 80.

This repository represents my end-to-end DevOps workflow — from local development to automated deployment.

---

# ✅ What I Implemented

## 1️⃣ Repository Setup

* Created a GitHub repository for the project.
* Pushed both frontend and backend source code.
* Organized project folders:

```
crud-dd-task-mean-app/
 ├── backend/
 ├── frontend/
 ├── nginx/
```

---

## 2️⃣ Containerization & Deployment

### Dockerization

I created Dockerfiles for:

* Backend (Node.js API)
* Frontend (Angular UI)

Then I built Docker images and pushed them to Docker Hub:

 commands : * docker build -t dd-backend ./backend
            * docker build -t dd-frontend ./frontend
            * docker tag dd-backend karthick2511/dd-backend:latest
            * docker push karthick2511/dd-backend
            * docker tag dd-frontend karthick2511/dd-frontend:latest
            * docker push karthick2511/dd-frontend

```
karthick2511/dd-backend
karthick2511/dd-frontend
```

### EC2 Setup

* Launched an Ubuntu VM on AWS EC2.
* Installed:

  * Docker
  * Docker Compose
* Pulled containers using docker-compose.

---

## 3️⃣ Database Setup

I used the official MongoDB Docker image as part of the Docker Compose stack.

MongoDB runs as a service container and connects internally with the backend.

Installing docker compose in VM
commands : sudo apt update
           sudo apt install docker.io docker-compose -y
           sudo usermod -aG docker $USER

Installing MongoDB  through docker-compose
commands : nano docker-compose.yml
           docker-compose up -d




## 4️⃣ Nginx Reverse Proxy

I configured Nginx inside a container to act as a reverse proxy.

### Responsibilities:

* Route traffic from port 80.
* Forward requests to frontend/backend services.
* Make the entire application accessible via:
```
http://<EC2_PUBLIC_IP>
```

---

## 5️⃣ CI/CD Pipeline (GitHub Actions)

I configured a GitHub Actions workflow inside:

```
.github/workflows/docker.yml
```

### What the pipeline does:

When I push code to `main`:

1. GitHub Actions runner starts automatically.
2. Backend and frontend Docker images are built.
3. Images are pushed to Docker Hub.
4. GitHub connects to my EC2 server via SSH.
5. Docker Compose pulls the latest images.
6. Containers restart with the new version.

This removed the need for manual deployment.

---

---

# 🧱 Project Architecture

```
Browser
   ↓
Nginx (Reverse Proxy)
   ↓
Frontend Container
   ↓
Backend Container
   ↓
MongoDB Container
```

GitHub Actions automates everything between GitHub → Docker Hub → EC2.

---

# ⚙️ Tech Stack

* Angular (Frontend)
* Node.js / Express (Backend)
* MongoDB
* Docker & Docker Compose
* Nginx
* GitHub Actions (CI/CD)
* AWS EC2 (Ubuntu)

---

# 📦 Deployment Workflow

My deployment process works like this:

1. I push changes to GitHub.
2. GitHub Actions builds new Docker images.
3. Images are pushed to Docker Hub.
4. GitHub connects to EC2 via SSH.
5. Containers automatically update.
6. Website refreshes with the new version.

---

# 🧪 Useful Commands

### Check running containers

```
docker ps
```

### Restart services

```
docker-compose down
docker-compose up -d
```

### View logs

```
docker logs nginx-container
```

---

# 🎯 What I Learned

* How to containerize a full-stack app.
* Building a CI/CD pipeline from scratch.
* Using GitHub Secrets securely.
* Reverse proxy setup using Nginx.
* Automating deployments to AWS EC2.

---

# 📎 Live Access

```
http://<EC2_ELASTIC_IP>
```

---


This project was completed as part of a DevOps internship task to demonstrate containerization, automation, and deployment practices.
