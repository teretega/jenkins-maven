pipeline {
    agent any

    environment {
        TOMCAT_SERVER = 'ec2-15-223-219-146.ca-central-1.compute.amazonaws.com'
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Deploy to Tomcat') {
            steps {
                sh '''
                    sudo cp /var/lib/jenkins/workspace/maven-pipline/src/main/webapp /opt/tomcat/webapps/
                    sudo chown tomcat:tomcat /opt/tomcat/webapps/emraay-bank-app.war
                    sudo systemctl restart tomcat
                '''
            }
        }
       }

    post {
        success {
            echo 'Deployment successfully!'
        }

        failure {
            echo 'Deployment failed!'
        }
    }
}
