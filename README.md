MY INTERNSHIP PROJECT 
CI/CD Pipeline Using GitHub Actions and Docker

1. Project Overview

This project demonstrates the implementation of an automated CI/CD (Continuous Integration and Continuous Deployment) pipeline using GitHub Actions and Docker.

The pipeline automatically builds and tests a web application whenever code is pushed to the GitHub repository. After successful testing, the Docker image is published to Docker Hub and deployed locally using Kubernetes through Minikube.

The main objective is to automate the software build, testing, image publishing, and deployment process without requiring cloud infrastructure.

2. Objectives

- Automate application building and testing.
- Create Docker images using Dockerfile.
- Manage containers using Docker Compose.
- Implement CI/CD using GitHub Actions.
- Store Docker images in Docker Hub.
- Deploy the application using Minikube.
- Understand Kubernetes Deployments and Services.

3. Technologies Used

Technology| Purpose
HTML, CSS, JavaScript| Frontend development
Git and GitHub| Version control
GitHub Actions| CI/CD automation
Docker| Containerization
Docker Compose| Container management
Docker Hub| Docker image registry
Kubernetes| Container orchestration
Minikube| Local Kubernetes cluster
YAML| Pipeline and Kubernetes configuration

4. Project Structure

ci-cd-docker-githubactions-project/
│
├── index.html
├── Dockerfile
├── docker-compose.yml
├── deployment.yaml
├── service.yaml
│
└── .github/
    └── workflows/
        └── ci-cd.yml

5. CI/CD Pipeline Workflow

The project follows these steps:

1. Developer pushes application code to GitHub.
2. GitHub Actions automatically triggers the workflow.
3. The application Docker image is built.
4. The Docker container is started for testing.
5. Automated testing checks whether the website responds successfully.
6. After successful testing, the Docker image is built for AMD64 and ARM64 platforms.
7. The image is pushed to Docker Hub.
8. Minikube pulls the Docker image.
9. Kubernetes deploys the application using two replicas.
10. A Kubernetes NodePort Service exposes the application.

6. Docker Implementation

Dockerfile

The Dockerfile uses Nginx as the base image and copies the HTML application into the Nginx web directory.

FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html

EXPOSE 80

Docker Compose

Docker Compose is used to build and run the application container.

docker compose up -d --build

To check running containers:

docker ps

7. GitHub Actions CI/CD

The GitHub Actions workflow is configured in:

".github/workflows/ci-cd.yml"

The workflow contains two jobs:

Job 1: Build and Test

- Checkout repository.
- Build Docker image.
- Run Docker container.
- Test website availability.
- Stop the test container.

Job 2: Push Image to Docker Hub

- Set up QEMU and Docker Buildx.
- Authenticate with Docker Hub using GitHub Secrets.
- Build multi-platform Docker image.
- Push the image to Docker Hub.

GitHub repository secrets used:

- DOCKERHUB_USERNAME
- DOCKERHUB_TOKEN

8. Docker Hub

The Docker image is published to Docker Hub.

Docker Image:

shivanis7/devops-cicd-app:latest

Pull the image using:

docker pull shivanis7/devops-cicd-app:latest

9. Kubernetes Deployment Using Minikube

Minikube is used to create a local Kubernetes cluster.

Start Minikube

minikube start --driver=docker

Deploy the application

kubectl apply -f deployment.yaml

Create Kubernetes Service

kubectl apply -f service.yaml

Verify Deployment

kubectl get deployments

Check Pods

kubectl get pods

Check Services

kubectl get services

Access the Application

minikube service devops-service

10. Expected Results

- GitHub Actions automatically builds and tests the application.
- Docker image is successfully published to Docker Hub.
- Kubernetes creates two application replicas.
- Minikube runs the application locally.
- The website is accessible through the Kubernetes Service.

11. Benefits

- Reduces manual deployment work.
- Improves software delivery speed.
- Provides automated application testing.
- Ensures consistent application packaging.
- Supports multi-platform Docker images.
- Demonstrates practical CI/CD and Kubernetes concepts.

12. Conclusion

This project demonstrates how CI/CD automation can simplify the software development and deployment process using GitHub Actions and Docker.

By integrating Docker Hub and Minikube, the project provides a complete local DevOps workflow, covering application building, automated testing, container image publishing, and Kubernetes deployment.

13. Author

Project: CI/CD Pipeline Using GitHub Actions and Docker

GitHub: https://github.com/shivanisakthivel/ci-cd-docker-githubactions-project

Docker Hub: https://hub.docker.com/r/shivanis7/devops-cicd-app
