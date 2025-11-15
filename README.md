# DevOps_TASK2

# Simple CI/CD Pipeline (Jenkins + Docker)

This project is a basic CI/CD setup that I built using **Jenkins** and **Docker**.

## 🔧 What I Did
- Created a `Jenkinsfile` with stages for build, test, Docker build, and deploy  
- Added a `Dockerfile` to containerize the application  
- Connected my GitHub repository to Jenkins  
- Set up a webhook so the pipeline runs automatically on every push  
- Tested the pipeline to ensure the app builds and deploys successfully  

## 🚀 Result
Whenever I push code to this repo, Jenkins automatically:
1. Pulls the latest code  
2. Installs dependencies  
3. Runs tests  
4. Builds a Docker image  
5. Deploys the app using Docker  

This completes the CI/CD workflow.

