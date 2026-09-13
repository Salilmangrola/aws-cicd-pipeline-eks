# aws-cicd-pipeline-eks
CI/CD pipeline to build and deploy a web application to Amazon EKS using AWS CodeBuild, Amazon ECR, and kubectl.


This repository provides an automated CI/CD and container orchestration workflow for deploying a web application to Amazon Elastic Kubernetes Service (Amazon EKS). The architecture leverages AWS-native developer tools—specifically AWS CodeBuild and Amazon Elastic Container Registry (ECR)—to containerize code directly from GitHub and deploy workloads into scalable Kubernetes Pods exposed via a public-facing Load Balancer.

Architecture & Workflow Steps

1. Infrastructure Setup (Amazon EKS):

An Amazon EKS cluster is provisioned alongside a managed worker node group backed by Amazon EC2 instances to handle the compute workload for Kubernetes pods.

2. Development & Version Control:

The application is developed locally (e.g., Visual Studio 2022) with necessary configuration files—including .gitignore, .dockerignore, Dockerfile, and buildspec.yml—and pushed to a GitHub repository.

3. Build & Containerization (AWS CodeBuild):

CodeBuild spins up a Linux-based build environment to execute the instructions defined in buildspec.yml. It runs standard Docker commands to build the application image and package runtime dependencies.

4. Image Registry (Amazon ECR):

Once successfully built, the Docker image is tagged and pushed to an Amazon ECR private repository for secure, low-latency container storage.

5. Deployment via kubectl:

Kubernetes manifests apply the deployment configurations to the EKS cluster, instructing the worker nodes to pull the latest container image from ECR and schedule the containerized Pods.

6. Ingress & Traffic Routing:

A Kubernetes LoadBalancer service provisions an AWS Load Balancer, providing an external DNS endpoint that routes inbound user traffic directly to the underlying application Pods.

7. Verification:

End users access the public DNS endpoint to interact with the deployed live web application.
