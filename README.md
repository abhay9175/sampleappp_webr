Deployment on AWS EKS

This project automates the build, push, and deployment of a Laravel application using GitHub Actions, Docker, and AWS EKS.

Workflow Overview

GitHub Actions Pipeline: 

Builds the Docker image from the modules/ folder.
Pushes the image to Docker Hub.
Connects to AWS EKS using kubectl.
Deploys the Laravel application using Kubernetes manifests.

Docker Build & Push:

The pipeline builds a Docker image using the Dockerfile inside the modules/ folder.
The image is pushed to Docker Hub under the repository your-dockerhub-username/laravel-app:latest.

Kubernetes Deployment:

kubectl apply is used to deploy k8s-deployment.yaml and k8s-service.yaml.
The application runs in AWS EKS and is exposed via a LoadBalancer.

Repository Structure:

/modules
  ├── Dockerfile
  ├── k8s-deployment.yaml
  ├── k8s-service.yaml
/.github/workflows
  ├── laravel-cicd.yml

How to Deploy Manually

Push changes to the main branch, and GitHub Actions will deploy automatically.
deploy using kubectl, run:

kubectl apply -f modules/k8s-deployment.yaml
kubectl apply -f modules/k8s-service.yaml

Check the deployment status:

kubectl get pods
kubectl get svc

Copy the EXTERNAL-IP of the service and open it in a browser.

Requirements

AWS EKS cluster configured
Docker installed and authenticated with Docker Hub
GitHub Actions Secrets configured for AWS and Docker

