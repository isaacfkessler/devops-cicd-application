# Sample application for DevOps Pipeline
## This is a sample application to demonstrate an end to end DevOps Pipeline

CI/CD Pipeline Documentation
Overview

This documentation provides an overview of the Continuous Integration and Continuous Deployment (CI/CD) pipeline for a Java application using Maven, Jenkins, SonarQube, and Docker.
Tools Used

    Java
    Maven
    Jenkins
    SonarQube
    Docker
    Docker Hub
    Git

CI/CD Pipeline Steps
1. Code Repository

The code is stored in a version-controlled repository (e.g., GitHub).
2. Continuous Integration (CI) with Jenkins
Jenkins Job: Build and Test

    Trigger: On code commit
    Actions:
        Jenkins pulls the code from the repository.
        Maven is used to build the Java application.
        Automated tests are executed.

Jenkins Job: SonarQube Analysis

    Trigger: After successful build and tests
    Actions:
        Jenkins triggers SonarQube analysis.
        SonarQube scans the code for quality issues.
        Results are sent to SonarQube server.

Jenkins Job: Quality Gate Check

    Trigger: After SonarQube analysis
    Actions:
        Jenkins checks the quality gate status on SonarQube.
        If the quality gate passes, the pipeline continues; otherwise, it fails.

3. Continuous Deployment (CD) with Docker
Jenkins Job: Build Docker Image

    Trigger: After successful quality gate check
    Actions:
        Jenkins builds a Docker image for the Java application.
        The Docker image is tagged with the Jenkins build version.

Jenkins Job: Push to Docker Hub

    Trigger: After Docker image build
    Actions:
        Jenkins pushes the Docker image to Docker Hub.
        The image is tagged with the Jenkins build version.

Versioning

The versioning follows the Jenkins build version. The Docker image and codebase are tagged with the same version to maintain consistency.
Environment Variables

    DOCKER_USER: Docker Hub username for image push.
    DOCKER_PASSWORD: Docker Hub password for image push.

Conclusion

This CI/CD pipeline automates the build, testing, code analysis, and Docker image creation for the Java application. The integration with SonarQube ensures code quality, and Docker facilitates easy deployment and distribution of the application.
