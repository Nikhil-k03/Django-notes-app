# Jenkins CI/CD Pipeline Project for Django Notes App

## Overview

This project demonstrates a complete end-to-end CI/CD pipeline implementation using Jenkins, Docker, Docker Compose, GitHub Webhooks, and AWS EC2.

The main goal of this project was to automate the software delivery process for a Dockerized Django Notes Application.

The pipeline automatically:

1. Pulls code from GitHub
2. Builds Docker images
3. Pushes Docker images to Docker Hub
4. Deploys the application using Docker Compose
5. Automatically triggers builds on every GitHub commit using Webhooks

This project also includes Jenkins Shared Libraries to make the pipeline modular and reusable.

---

# Architecture

```text
Developer Pushes Code to GitHub
                ↓
        GitHub Webhook Trigger
                ↓
            Jenkins Server
                ↓
         Jenkins Agent Node
                ↓
          Docker Image Build
                ↓
        Push Image to Docker Hub
                ↓
       Docker Compose Deployment
                ↓
        Django Notes App on AWS EC2
```

---

# Tech Stack

## Cloud & Infrastructure

* AWS EC2
* Ubuntu Linux
* Security Groups
* SSH

## DevOps Tools

* Jenkins
* Jenkins Shared Libraries
* GitHub Webhooks
* Docker
* Docker Compose
* Docker Hub

## CI/CD

* Jenkins Declarative Pipeline
* Automated Build & Deployment

## Application

* Django
* Python
* SQLite
* Gunicorn
* Nginx

---

# Features Implemented

## Jenkins Master-Agent Architecture

* Configured Jenkins master server
* Connected Jenkins agent node
* Executed builds on agent node
* Used labels for agent-based pipeline execution

## Automated CI/CD Pipeline

* GitHub integration
* Automatic code cloning
* Docker image build automation
* Docker image push to Docker Hub
* Automated deployment using Docker Compose

## Dockerization

* Created Dockerfile for Django application
* Containerized application
* Optimized Docker build
* Removed unnecessary MySQL dependencies

## Docker Compose Deployment

* Multi-container deployment setup
* Nginx reverse proxy integration
* Container orchestration using Docker Compose

## GitHub Webhook Integration

* Configured automatic Jenkins trigger on every GitHub push
* Enabled fully automated CI/CD flow

## Jenkins Shared Libraries

* Created reusable Groovy functions
* Modularized pipeline logic
* Implemented reusable build and clone stages

---

# Project Structure

```text
Django-notes-app/
│
├── Dockerfile
├── docker-compose.yml
├── Jenkinsfile
├── requirements.txt
├── manage.py
├── notesapp/
├── nginx/
└── db.sqlite3
```

---

# Jenkins Shared Library Structure

```text
jenkins-shared-libraries/
│
├── vars/
│   ├── clone.groovy
│   ├── buildDocker.groovy
│   └── docker_push.groovy
```

---

# CI/CD Workflow

## Step 1: Developer Pushes Code

Whenever code is pushed to GitHub, GitHub Webhook automatically triggers the Jenkins pipeline.

## Step 2: Jenkins Pipeline Starts

Jenkins pulls the latest code from the GitHub repository.

## Step 3: Docker Image Build

The pipeline builds a Docker image for the Django application.

## Step 4: Push Image to Docker Hub

The newly built image is pushed to Docker Hub using Jenkins credentials.

## Step 5: Deploy Application

Docker Compose deploys the updated application automatically on the EC2 instance.

---

# Jenkins Pipeline Stages

## 1. Clone Stage

* Clones code from GitHub repository
* Uses shared library clone function

## 2. Build Stage

* Builds Docker image
* Uses reusable shared library function

## 3. Push Stage

* Pushes Docker image to Docker Hub
* Uses Jenkins credentials securely

## 4. Deploy Stage

* Deploys containers using Docker Compose
* Updates running application automatically

## 5. Cleanup Stage

* Removes unused Docker images and containers
* Prevents storage issues on EC2 instance

---

# Challenges Faced During the Project

## 1. Docker Storage Issues

### Problem:

Docker images and containers consumed most of the EC2 storage causing build failures.

### Solution:

* Used Docker cleanup commands
* Implemented Docker prune operations
* Optimized Dockerfile
* Removed unnecessary dependencies

---

## 2. Port Allocation Errors

### Problem:

Port 8000 was already occupied by old containers.

### Solution:

* Added container cleanup before deployment
* Removed old containers before starting new ones

---

## 3. MySQL Dependency Errors

### Problem:

The application initially used MySQL configuration which caused dependency and build issues.

### Solution:

* Migrated project from MySQL to SQLite
* Removed MySQL-related dependencies
* Simplified Docker build process

---

## 4. Jenkins Shared Library Issues

### Problem:

Shared library functions failed because of incorrect Groovy syntax and naming mismatches.

### Solution:

* Corrected Groovy function definitions
* Standardized reusable function naming
* Properly configured Jenkins Global Shared Libraries

---

## 5. Webhook Trigger Issues

### Problem:

GitHub webhook initially failed to trigger Jenkins builds.

### Solution:

* Configured GitHub webhook properly
* Opened required ports in AWS Security Groups
* Enabled Jenkins webhook trigger settings

---

# Security Implementations

* Jenkins credentials used for Docker Hub authentication
* Secrets were not hardcoded in the pipeline
* AWS Security Groups configured properly
* Secure GitHub webhook communication

---

# Key Learnings From This Project

## DevOps Concepts Learned

* CI/CD automation
* Jenkins pipelines
* Jenkins shared libraries
* Docker containerization
* Docker Compose orchestration
* GitHub webhook automation
* AWS EC2 deployment
* Linux troubleshooting
* Infrastructure debugging

## Practical Skills Developed

* Real-world debugging
* Production-like deployment workflow
* Container management
* Pipeline troubleshooting
* Storage optimization
* Build automation

---

# Conclusion

This project helped in understanding real-world DevOps workflows and CI/CD automation.

The project provided practical exposure to:

* Cloud infrastructure
* Jenkins automation
* Docker ecosystem
* Deployment strategies
* DevOps troubleshooting

It also improved debugging and infrastructure management skills by solving real deployment and configuration issues during development.
