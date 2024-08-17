# vprofile Project CI/CD Pipelines

This repository contains the Continuous Integration and Continuous Deployment (CI/CD) pipelines for the java web application project. The pipelines automate the process of building, testing, analyzing, and deploying the application to both staging and production environments.

## Pipelines Overview

### Staging Pipeline

The **Staging Pipeline** is designed for testing and validation in a staging environment before production deployment. It includes the following stages:

1. **Build**: Compiles the application and packages it into a WAR file.
2. **Test**: Runs unit tests to ensure code quality.
3. **Checkstyle Analysis**: Performs code style checks using Checkstyle.
4. **Sonar Analysis**: Conducts static code analysis using SonarQube to identify code smells, bugs, and vulnerabilities.
5. **Quality Gate**: Waits for SonarQube's quality gate to pass; if it fails, the pipeline is aborted.
6. **Upload Artifact**: Uploads the built WAR file to a Nexus repository.
7. **Build App Image**: Creates a Docker image for the application.
8. **Upload Image to ECR**: Pushes the Docker image to AWS Elastic Container Registry (ECR).
9. **Deploy to ECS Staging**: Deploys the Docker image to an AWS ECS staging cluster.

Notifications are sent to a Slack channel upon completion of the pipeline.

### Production Pipeline

The **Production Pipeline** handles the deployment of the application to the production environment. It includes the following stage:

1. **Deploy to ECS Prod**: Updates the ECS service in the production cluster to use the latest Docker image.

Notifications are also sent to a Slack channel upon completion of this pipeline.

## Setup and Configuration

To use these pipelines, follow these steps:

1. **Install Jenkins Plugins**:
   - Maven Integration
   - Docker Pipeline
   - SonarQube Scanner for Jenkins
   - AWS Steps
   - Nexus Artifact Uploader
   - Slack Notification

2. **Configure Jenkins Tools**:
   - Maven: `MAVEN3`
   - JDK: `OracleJDK8`
   - SonarQube Scanner: `sonarscanner`

3. **Setup Jenkins Credentials**:
   - AWS Credentials: `awscreds`
   - Nexus Credentials: `nexuslogin`
   - Docker Registry Credentials: `ecr:us-east-1:awscreds`

4. **Configure SonarQube**: Ensure the SonarQube server and scanner are correctly set up in Jenkins.

5. **Setup Nexus**: Verify that the Nexus repository settings match the pipeline configurations.

![image](https://github.com/user-attachments/assets/9347a966-5269-4e57-b1a7-d529ac77da9e)

![image](https://github.com/user-attachments/assets/f70cdecb-3fec-4aeb-97ed-9f0e79aa37fd)
![image](https://github.com/user-attachments/assets/6c531f66-0b12-4d8a-884c-ed6d4343aecc)





