# Microservices Deployment with Helm and Amazon ECR

This repository contains the configuration and scripts to deploy microservices using EKS Cluster with Helm charts and Container images from Amazon Elastic Container Registry (ECR).

## Table of Contents
- Prerequisites
- Setup
- Create EKS Cluster using eksctl
- Building and Pushing Docker Images
- Deploying with Helm
- Exposing with Ngrok

## Prerequisites
- Docker installed on your local machine.
- eksctl & kubectl client installed.
- AWS CLI configured with appropriate permissions.
- Helm installed (version 3.8.0 or higher).
- Signup Ngrok Free account for API & AUTH_Token Keys.

## Setup
1. **Clone the repository:**
    ```sh
    git clone https://github.com/Alex-philip5/alex-microservices.git
    cd alex-microservices
    ```
2. **Create EKS Cluster using eksctl:**
    ```sh
    eksctl create cluster -f eks-cluster.yaml
    aws eks update-kubeconfig --region ap-south-1 --name eks-demo-cluster
    kubectl cluster-info
    kubectl get nodes
    kubectl get po -n kube-system


2. **Authenticate Docker to your Amazon ECR registry:**
    ```sh
    aws ecr get-login-password --region your-region | docker login --username AWS --password-stdin your-account-id.dkr.ecr.your-region.amazonaws.com
    ```

## Building and Pushing Docker Images
1. **Build your Docker image using Docker-Compose:**
    ```sh
    cd alex-microservices/src
    docker-compose build
    ```

2. **Tag the Docker image:**
    ```sh
    docker tag your-image-name:latest your-account-id.dkr.ecr.your-region.amazonaws.com/your-repo-name:latest
    ```

3. **Push the Docker image to ECR:**
    ```sh
    docker push your-account-id.dkr.ecr.your-region.amazonaws.com/your-repo-name:latest
    ```

## Deploying ECR Image with Helm
1. **Deploy the Helm repository:**
    ```sh
    helm install fe-helm-app fe-helm
    ```

## Expose the application using Ngrok
1. **Expose application using Ngrok
    ```sh
    kubectl apply -f game-service.yaml
    kubectl apply -f game-deployment.yaml
    k apply -f game-ingress.yaml
    ```

