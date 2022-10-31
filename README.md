# Monolith to Microservices

Udagram is a simple cloud application developed alongside the Udacity Cloud Engineering Nanodegree. It allows users to register and log into a web client, post photos to the feed, and process photos using an image filtering microservice.

## Prerequisites

### Docker

Instructions for installing Docker can be found [here](https://docs.docker.com/install/).

### Kubernetes

#### Kubernetes Cluster

- Minikube: Instructions for installing Minikube can be found [here](https://kubernetes.io/docs/tasks/tools/install-minikube/)
- KubeOne: Instructions for installing KubeOne can be found [here](https://github.com/kubermatic/kubeone) (Linux and macOS only)
- Docker Desktop: For macOS and Windows it is recommended to install Kubernetes by enabling it in Docker Desktop

#### Kubernetes CLI

It is recommended to use kubectl for managing the Kubernetes cluster. Intructions for installing kubectl can be found [here](https://kubernetes.io/docs/tasks/tools/install-kubectl).

### Travis CI

Instructions for installing Travis CI with a GitHub repository can be found [here](https://docs.travis-ci.com/user/tutorial/).

## Dependencies

- Amazon Web Services S3 - Bucket for image storage
- Amazon Web Services RDS - Postgres database instance
- Amazon Web Services IAM account (optional)

## Getting Started

### Settings

The following settings are required by the application:
- AWS_BUCKET - S3 bucket name
- AWS_REGION - AWS region
- AWS_PROFILE - AWS profile
- JWT_SECRET - JWT token secret
- POSTGRESS_DB - Postgres database name
- POSTGRESS_HOST - URL of Postgres database instance
- POSTGRESS_PASSWORD - Database password
- POSTGRESS_USERNAME - Database username
- URL - Application URL

###  Docker Environment

Open a new terminal within the project directory and run:
1. Build the images: `docker-compose -f docker-compose-build.yaml build --parallel`
2. Push the images: `docker-compose -f docker-compose-build.yaml push`
3. Start the containers: `docker-compose up`

### Kubernetes Environment

1. Setup secret keys and configmaps (aws-secret, env-secret, env-configmap)
2. Apply secret keys and configmap: `kubectl apply -f aws-secret.yaml -f env-secret.yaml -f env-configmap.yaml`
3. Apply deployments: `kubectl apply -f backend-feed-deployment.yaml -f backend-user-deployment.yaml -f frontend-deployment.yaml -f reverseproxy-deployment.yaml`
4. Apply services: `kubectl apply -f backend-feed-service.yaml -f backend-user-service.yaml -f frontend-service.yaml -f reverseproxy-Service.yaml`

### Travis CI

1. Setup environment variables for Docker Hub credentials
2. Setup application environment variables (as above)
3. Push latest changes to the repository
4. Build application with Travis CI

## Acknowledgements

This project was bootstrapped with [https://github.com/scheeles/cloud-developer/tree/06-ci/course-03/exercises](https://github.com/scheeles/cloud-developer/tree/06-ci/course-03/exercises).
