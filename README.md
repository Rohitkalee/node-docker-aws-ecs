# AWS DevOps: CI/CD Pipeline for Containers on AWS using CodePipeline, CodeBuild, ECR, and ECS

## Solution architecture

The following diagram shows the flow of events in the solution:

![AWS DevOps: CI/CD Pipeline for Containers on AWS using CodePipeline, CodeBuild, ECR, and ECS]


## Getting Started 

### Prerequisites

Before we dive into the details of the deployment pipeline, make sure you have the following prerequisites in place:

- **AWS account**: With permissions to create resources specified in the code.
- **Fork GitHub Repo**: Fork and clone your own [Yris-ops/aws-devops-continuous-docker-deployment-to-aws-fargate](https://github.com/Yris-ops/aws-devops-continuous-docker-deployment-to-aws-fargate) GitHub repository.
- **GitHub Token**: Create an token in GitHub and provide access to the repo scopes.
- **Terraform**: Installed on your local machine.
- **Docker**: Installed on your local machine.

### Implementation 

Terraform: All the resource provisioning for this solution is written in a Terraform configuration, which is available in the GitHub repository.

### Deployment Steps

1. **Clone** this repo on the local machine.
1. **Fork** this repo on your GitHub account.
1. **Modify** the necessary parameters in the vars.tf file to suit your needs, such as region, VPC parameters, GitHub token, nomenclatures, etc.
1. **Deploy** the Terraform configuration with the following command: `terraform init && terraform apply --auto-approve`.
1. **Wait** 5 to 10 minutes until all resources are deployed.

### Key Components for Continuous Deployment on AWS Fargate

1. **Virtual Private Cloud (VPC)**: 

![AWS DevOps: Continuous Docker Deployment to AWS Fargate from GitHub using Terraform](./img/img1.png)

The VPC defines an isolated network in the cloud where you can deploy your AWS resources. It's used to host your subnets, security groups, alb, and other networking resources.

2. **Subnets**: 

![AWS DevOps: Continuous Docker Deployment to AWS Fargate from GitHub using Terraform](./img/img2.png)

Subnets are logical partitions of your VPC network that can be spread across different availability zones to ensure high availability of your resources. A minimum of 2 AZ is required for alb deployment and resilient architecture.

3. **Internet Gateway**: 

![AWS DevOps: Continuous Docker Deployment to AWS Fargate from GitHub using Terraform](./img/img3.png)

The internet gateway enables your resources in the VPC to communicate with the internet.

4. **NAT Gateway**: 

![AWS DevOps: Continuous Docker Deployment to AWS Fargate from GitHub using Terraform](./img/img4.png)

The NAT Gateway allows resources in private subnets to access the internet without directly exposing those resources.

5. **Route Tables**: 

![AWS DevOps: Continuous Docker Deployment to AWS Fargate from GitHub using Terraform](./img/img5.png)

Route tables define how network traffic is directed between different resources within your VPC.

6. **Security Groups**: 

![AWS DevOps: Continuous Docker Deployment to AWS Fargate from GitHub using Terraform](./img/img6.png)

Security groups are virtual firewalls that control incoming and outgoing traffic for your instances. They act as instance-level firewalls.

7. **Elastic Container Service (ECS)**: 

![AWS DevOps: Continuous Docker Deployment to AWS Fargate from GitHub using Terraform](./img/img7.png)

ECS is a container management service that enables you to run and manage containerized applications. It offers flexible deployment options for Docker containers.

8. **ECS Cluster**: 

![AWS DevOps: Continuous Docker Deployment to AWS Fargate from GitHub using Terraform](./img/img8.png)

An ECS cluster is a group of EC2 or Fargate resources that allows you to run containerized tasks and services.

9. **Task Definition**: 

![AWS DevOps: Continuous Docker Deployment to AWS Fargate from GitHub using Terraform](./img/img9.png)

The ECS task definition is a template for defining how a containerized application should run, including Docker images, exposed ports, etc.

10. **IAM Roles and Policies**: 

IAM (Identity and Access Management) is used to manage roles and permissions. In my case, roles and policies are created to 
allow services to authenticate and access other services.

11. **CodePipeline**: 

![AWS DevOps: Continuous Docker Deployment to AWS Fargate from GitHub using Terraform](./img/img10.png)

AWS CodePipeline is a continuous deployment service that automates the process of releasing your code changes. It coordinates actions 
such as building, testing, and deploying.

![AWS DevOps: Continuous Docker Deployment to AWS Fargate from GitHub using Terraform](./img/img11.png)

12. **CodeBuild**:

![AWS DevOps: Continuous Docker Deployment to AWS Fargate from GitHub using Terraform](./img/img12.png)

AWS CodeBuild is a fully managed build service that compiles your code, runs tests, and produces deployable artifacts.

13. **S3 (Amazon Simple Storage Service)**: 

![AWS DevOps: Continuous Docker Deployment to AWS Fargate from GitHub using Terraform](./img/img13.png)

S3 is a scalable object storage service used to store build artifacts.

14. **CloudWatch Events**: CloudWatch Events allows you to monitor and respond to changes in the state of AWS resources. In case, it's used to detect changes in CodeBuild build statuses.

15. **SNS (Simple Notification Service)**: 

![AWS DevOps: Continuous Docker Deployment to AWS Fargate from GitHub using Terraform](./img/img14.png)

Subscribers to this topic can receive notifications via email, allowing them to stay informed about the status of deployments.

16. **Load Balancer (ALB)**: 

![AWS DevOps: Continuous Docker Deployment to AWS Fargate from GitHub using Terraform](./img/img15.png)

The Application Load Balancer (ALB) distributes incoming traffic across different IPs of your application based on defined routing rules.

17. **Target Groups**: 

![AWS DevOps: Continuous Docker Deployment to AWS Fargate from GitHub using Terraform](./img/img16.png)

Target groups are used with the load balancer to direct traffic to specific instances based on defined criteria.

18. **GitHub Token**: 

![AWS DevOps: Continuous Docker Deployment to AWS Fargate from GitHub using Terraform](./img/img17.png)

GitHub token with repository access rights.

19. **To Access Application**:

- Copy and paste the Terraform deployment output in your favorite browser.

![AWS DevOps: Continuous Docker Deployment to AWS Fargate from GitHub using Terraform](./img/img18.png)

- Go to the AWS Management Console and navigate to the EC2 service and go on Load Balancer section. You can access the application by copy and paste the ALB DNS.

### Let's take a look at the application

![AWS DevOps: Continuous Docker Deployment to AWS Fargate from GitHub using Terraform](./img/img19.png)

### Test Deployment

1. Modify your application's app.py file. Change what you want in the code, text, color, font, text size, etc… Save the changes.
1. Commit the modification to your Github repository.
1. Wait a few minutes for the new tasks to run and go to the ALB DNS to see your application update.

You can follow the update in the CodeBuild and CodePipeline services.

![AWS DevOps: Continuous Docker Deployment to AWS Fargate from GitHub using Terraform](![Uploading image.png…]()


## CleanUp Resources

To clean up the Terraform deployment, you can follow these steps:

1. Open the AWS Management Console and navigate to the S3 Bucket service and empty your S3 Bucket.
1. Navigate to the ECR Repository service and delete your repository.
1. To remove the resources created by this Terraform main.tf, run the following command: terraform destroy --auto-approve
1. Wait the deletion to complete, it may take some time to remove all the resources.

## Conclusion

Implementing a Continuous Docker Deployment pipeline to AWS Fargate from a GitHub repository using Terraform empowers development teams to deliver software efficiently and reliably. Automation reduces the risk of human error and ensures that code changes are quickly and consistently deployed to production environments.

By following the steps outlined in this article, you'll establish a robust deployment process that leverages the power of AWS services, Docker containers, and infrastructure-as-code principles. This approach sets the stage for faster development cycles, better collaboration, and increased confidence in your application deployments.

## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This repository is licensed under the Apache License 2.0. See the LICENSE file.
