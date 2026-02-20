# React Tetris V1

Tetris game built with React

<h1 align="center">
  <img alt="React tetris " title="#React tetris desktop" src="./images/game.jpg" />
</h1>


# 🎮 TETRIS DevSecOps CI/CD with ArgoCD – Deployment Steps

1. Launch an AWS EC2 instance (Ubuntu 24.04, t2.large, 50GB) and attach an IAM Role with Admin access.

2. Install required tools on EC2: Java (Temurin 17), Jenkins, Docker, SonarQube (via Docker), AWS CLI, kubectl, Terraform, and Trivy.

3. Start SonarQube container:

4. Configure Jenkins:
   - Install plugins (JDK, SonarQube Scanner, NodeJS, OWASP, Docker)
   - Add Sonar token in credentials
   - Add DockerHub credentials
   - Add GitHub token

5. Create Jenkins pipeline for EKS provisioning using Terraform:
   - terraform init
   - terraform validate
   - terraform plan
   - terraform apply
   (This creates VPC, subnets, EKS cluster, and node group.)

6. Create Jenkins pipeline for Tetris application:
   - Checkout source code
   - Run SonarQube analysis
   - Enforce Quality Gate
   - Run npm install
   - Perform Trivy security scan
   - Build Docker image
   - Push image to DockerHub
   - Update deployment.yml in manifest repository

7. Update kubeconfig to connect Jenkins to EKS:
   

8. Install ArgoCD in EKS:
  

9. Login to ArgoCD, connect the manifest repository, create a new application, and enable automatic sync.

10. Access the application using:
    
    Open the LoadBalancer hostname in the browser.

11. For Version 2 deployment:
    - Push updated code to V1 repository
    - Jenkins builds new Docker image
    - Updates deployment.yml
    - ArgoCD automatically syncs and deploys the new version.
