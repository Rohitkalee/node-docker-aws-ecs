# 🚀 CI/CD Pipeline for Containers on AWS

This project demonstrates a **Continuous Integration (CI) and Continuous Deployment (CD)** pipeline for containerized applications using AWS Developer Tools and ECS.

---

## 📌 Architecture Overview

<img width="800" height="400" alt="image" src="https://github.com/user-attachments/assets/6888203e-5532-495a-90a1-dc0fd627b2fc" />


The pipeline automates the process of building, storing, and deploying containerized applications using the following AWS services:

1. **CodeCommit** – Source code repository where developers push application code.  
2. **CodePipeline** – Orchestrates the CI/CD workflow.  
3. **S3 Bucket** – Stores pipeline artifacts.  
4. **CodeBuild** – Builds Docker images from source code and pushes them to Amazon ECR.  
5. **ECR (Elastic Container Registry)** – Stores built Docker images.  
6. **CodeDeploy** – Handles deployment to ECS using blue/green or rolling deployment strategies.  
7. **ECS Cluster** – Runs the containerized application using Fargate or EC2 launch type.  
8. **Users** – Access the deployed application via ECS service (usually through a Load Balancer).  

---

## ⚙️ Workflow Steps

1. Developer pushes code to **CodeCommit**.  
2. **CodePipeline** is triggered and fetches the latest changes.  
3. Artifacts are stored in an **S3 bucket**.  
4. **CodeBuild** builds the Docker image using `Dockerfile`.  
5. The image is pushed to **Amazon ECR**.  
6. **CodePipeline** triggers **CodeDeploy**.  
7. **CodeDeploy** updates the running tasks in the **ECS Cluster**.  
8. Users access the updated application.  

---

## 🛠️ AWS Services Used

- **AWS CodeCommit**  
- **AWS CodePipeline**  
- **AWS CodeBuild**  
- **Amazon S3**  
- **Amazon ECR**  
- **AWS CodeDeploy**  
- **Amazon ECS (Fargate/EC2)**  

---

## 🚦 Deployment Strategy

You can use either:  
- **Rolling deployment** – Gradually replace old tasks with new ones.  
- **Blue/Green deployment** – Create a new environment and shift traffic after validation.  

---

## 📂 Files to Include

- `Dockerfile` → Defines container build instructions.  
- `buildspec.yml` → CodeBuild build instructions.  
- `appspec.yml` → CodeDeploy deployment configuration.  
- `taskdef.json` → ECS task definition.  

---

## ✅ Benefits

- Automated builds and deployments  
- Faster release cycle  
- Scalable and reliable infrastructure  
- Zero-downtime deployment with Blue/Green  

---

## 👤 Author

Created as a reference for setting up **CI/CD pipelines for containers on AWS**.

