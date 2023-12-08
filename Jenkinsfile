pipeline{
    agent any
    tools {
        jdk 'Java17'
        maven 'Maven3'
    }


    stages{
        stage("Cleanup Workspace"){
            steps{
                cleanWs()
            }
        }
    }

    stages{
        stage("Checkout from SCM"){
            steps{
                git branch: 'main', credentialsId: 'github-credentials', url: 'https://github.com/isaacfkessler/devops-cicd-application' // this step specified branch, and credentials and git repository url
            }
        }
    }    
}
