# Jenkins CI/CD Pipeline Demo (GitHub + Docker)

A portfolio mini project demonstrating an end-to-end CI/CD pipeline using **Jenkins Pipeline (Jenkinsfile)**.
On every change to the `main` branch, Jenkins pulls the code from GitHub, builds a Docker image, and deploys it as a running container.

## Tech Stack
- Jenkins (Pipeline as Code)
- Git & GitHub
- Docker
- Nginx (serving a simple HTML page)
# How it works (CI/CD)
1. Developer pushes code to GitHub (main branch)
2. Jenkins pipeline runs:
   - Checkout source
   - Build Docker image
   - Deploy container
3. App becomes available at: `http://localhost:8090`

## Local run (without Jenkins)
```bash
docker build -t demo .
docker run -d --name demo -p 8090:80 demo
