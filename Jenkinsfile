pipeline {

    agent any 

    tools {
        maven 'M2_HOME'
    }

    environment {
        
        registry = "211125431540.dkr.ecr.us-east-1.amazonaws.com/devops_repository"
        registryCredential = 'jenkins-ecr'
        dockerImage = ''
        region = 'us-east-1'
    }

    stages {
    
        stage('Checkout'){
            steps {

                git branch: 'main', url: 'https://github.com/EVT98/jenkins-project-3-devops-ci.git'
            }
        }


        stage('Build') {
            steps {
                sh 'mvn clean'
                sh 'mvn compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package -DskipTests'
            }
        }

        stage('Build image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }

        stage('Docker login') {
            steps {
                script {
                    sh 'aws ecr get-login-password --region "${region}"| docker login --username AWS --password-stdin "${registry}"'
                }
            }
        }

        stage('Deploy Image') {
            steps {
                script {
                    dockerImage.push()
                }
            }
        }


    }
}