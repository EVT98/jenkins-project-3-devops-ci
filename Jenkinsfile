pipeline {

    agent any 

    tools {
        maven 'M2_HOME'
    }


    stages {

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

        stage('Deploy') {
            steps {
                echo 'Deploy step'
                sleep 10
            }
        }

        stage('Docker') {
            steps {
                echo 'image step'
            }
        }


    }
}