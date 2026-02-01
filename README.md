# Automated Website Deployment (CI/CD Pipeline)

## Overview
This project demonstrates a complete **CI/CD pipeline** that automatically builds and deploys a static website using **GitHub, Jenkins, and Docker**.

The purpose of this project is to showcase:
- Jenkins Declarative Pipelines
- Docker image building and container lifecycle management
- Integration between GitHub (source control), Jenkins (CI/CD), and Docker (runtime)

---

## Architecture & Workflow

1. Code is pushed to GitHub
2. Jenkins pulls the latest commit from the repository
3. Jenkins builds a Docker image using a Dockerfile
4. Any existing container is stopped and removed
5. A new container is started with the updated image
6. The website is served via Apache HTTPD inside Docker

---

## Technologies Used

- **Jenkins** – CI/CD automation
- **Docker** – Containerization and deployment
- **Apache HTTPD (`httpd:2.4`)** – Web server
- **GitHub** – Source control management

---

## Project Structure
├── Dockerfile
├── Jenkinsfile
├── index.html
└── README.md

---

## Dockerfile

```dockerfile
This Dockerfile builds a lightweight image that serves a static HTML website using Apache HTTPD.


Jenkins Pipeline

The pipeline is defined in Jenkinsfile and performs the following stages:

Docker sanity check – validates Docker availability

Build image – builds the Docker image from the Dockerfile

Stop old container – removes any existing container

Run container – starts a new container with port mapping



What Works Successfully

Jenkins correctly pulls the latest code from GitHub

Pipeline stages execute in the correct order

Docker containers are created, stopped, and restarted automatically

The website updates when the pipeline rebuilds in an unrestricted network

CI/CD logic is correct and reproducible




Known Issue: Docker Hub Access in China

When running this project from Mainland China, Docker image pulls may fail with errors such as:

failed to resolve reference docker.io/library/httpd:2.4
connection reset by peer
failed to fetch anonymous token
EOF

Root Cause

Docker Hub endpoints such as:

registry-1.docker.io

auth.docker.io

are partially blocked or unstable in Mainland China.
This prevents Docker from pulling base images like httpd:2.4.

This is a network and location restriction, not a pipeline or configuration issue.

Why This Is Not a Code Issue:

GitHub repository cloning works correctly

Jenkins pipeline executes correctly

Docker commands function when network access is available

Errors occur only during Docker Hub image pull requests

The CI/CD implementation itself is correct.

How This Would Be Solved in Production

In real-world environments, this issue would be handled by:

Using Docker registry mirrors (Alibaba Cloud, DaoCloud)

Hosting a private Docker registry

Pre-building base images

Running CI/CD infrastructure outside restricted networks

Using cloud-based CI/CD services (AWS, GitHub Actions, GCP)

Conclusion

This project successfully demonstrates a functional CI/CD pipeline using Jenkins and Docker.

Any deployment limitations encountered are due to regional networking restrictions rather than design or implementation flaws. The pipeline logic and automation flow are production-aligned and correct.