pipeline{
    agent any
    tools {
        jdk 'Java17'
        maven 'Maven3'
    }
environment {
    APP_NAME = "cicd-application"
    RELEASE = "1.0.0"
    DOCKER_USER = "isaacfkessler"
    DOCKER_PASS = 'dockerhub'
    IMAGE_NAME = "${DOCKER_USER}" + "/" + "${APP_NAME}"
    IMAGE_TAG = "${RELEASE}-${BUILD_NUMBER}"


}

    stages{
        stage("Cleanup Workspace"){
            steps{
                cleanWs()
            }
        }

        stage("Checkout from SCM"){
            steps{
                git branch: 'main',credentialsId: 'github-credentials', url: 'https://github.com/isaacfkessler/devops-cicd-application' // this step specified branch, and credentials and git repository url
            }
        }

        stage("Build App"){
            steps{
                sh "mvn clean package"
            }
        }

        stage("Test App"){
            steps{
                sh "mvn test"
            }
        }

        stage("Sonar Analysis"){
            steps{
                script{
                    withSonarQubeEnv(credentialsId: 'sonarqube-id') {
                        sh "mvn sonar:sonar"
                    }
                }
            }   
        }

        stage("Quality Gate Analysis"){
            steps{
                script{
                    waitForQualityGate abortPipeline: false, credentialsId: 'sonarqube-id'
                }
            }   
        }        

        stage("Build Image and Push"){
            steps{
                script{
                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image = docker.build "${IMAGE_NAME}"
                    }

                    docker.withRegistry('',DOCKER_PASS) {
                        docker_image.push("${IMAGE_TAG}")
                        docker_image.push("latest")
                    }
                }
            }   
        }         
    }    
}

