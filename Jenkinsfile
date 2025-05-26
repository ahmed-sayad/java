@Library('sharedlib') _

pipeline {
    agent any

    environment {
        MAVEN_HOME = tool 'M3'
        PATH = "${MAVEN_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Clone') {
            steps {
                echo 'Cloning done by Jenkins'
            }
        }

        stage('Build the project') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Test the project') {
            steps {
                script {
                    try {
                        sh 'mvn test'
                    } catch (err) {
                        echo "Tests failed or not found, continuing pipeline"
                    }
                }
            }
        }

        stage('Docker Build & Push') {
            steps {
                script {
                    docker.buildAndPush("ahmedelsayad/java-app")
                }
            }
        }
    }
}
