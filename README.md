# Static Website Hosting on AWS EC2 with Docker

This project demonstrates how to host a static website on AWS EC2 using Docker and Terraform. The workflow involves creating infrastructure with Terraform, building and pushing Docker images, and deploying the container on EC2.

## Project Overview

1. **Docker Hub Repository**: Store and pull Docker images.
2. **AWS EC2 Instance**: Provisioned using Terraform.
3. **Docker Image**: Built from a Dockerfile and pushed to Docker Hub.
4. **Automation**: Terraform automates EC2 setup and Docker image handling.
5. **Deployment Script**: A `build-docker-image.sh` script automates building the Docker image and deploying the website on EC2.

## Prerequisites

- AWS account with necessary permissions
- Docker installed locally
- Terraform installed
- Docker Hub account

## Project Structure

```
├── Dockerfile                  # Instructions to build Docker image
├── build-docker-image.sh       # Script to build and push Docker image and deploy to EC2
├── ec2.tf                     # Terraform configuration
└── README.md                   # Project documentation
```

## Setup Instructions

### 1. Clone the Repository

```bash
git clone <your-repo-url>
cd <your-repo-folder>
```

### 2. Configure Docker Hub

Log in to Docker Hub:

```bash
docker login
```

Ensure your `Dockerfile` and `build-docker-image.sh` scripts are correctly set up to build and push the image.

### 3. Deploy Infrastructure with Terraform

Initialize and apply Terraform configuration:

```bash
terraform init
terraform apply
```

Access the public IP of the EC2 instance from the Terraform output to view the website.

### 4. Verify Deployment

Check if the Docker container is running on the EC2 instance:

```bash
ssh -i <your-key.pem> ec2-user@<ec2-public-ip>
docker ps
```

## Troubleshooting

1. **Enable Terraform Logs**

Set the log path for Terraform to capture debug information:

```bash
export TF_LOG_PATH=./terraform_debug.log
```

2. **Ensure Non-Interactive Package Installation**

When installing software on the EC2 instance via Terraform, always use the `-y` flag to avoid prompts that cause Terraform to hang. Example:

```bash
sudo yum install -y docker
```

## Cleanup

To tear down the infrastructure:

```bash
terraform destroy
```

## Future Improvements

- Automate Docker image builds with CI/CD
- Enhance security with EC2 IAM roles and least privilege
- Implement monitoring with CloudWatch



