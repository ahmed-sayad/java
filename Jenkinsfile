@Library('sharedlib') _

pipeline {
    agent any

    environment {
        MAVEN_HOME = tool 'M3'
        PATH = "${MAVEN_HOME}/bin:${env.PATH}"
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                script {
                    try {
                        sh 'mvn test'
                    } catch (err) {
                        echo "Tests failed"
                    }
                }
            }
        }

        stage('Docker Build & Push') {
            steps {
                script {
                    buildAndPush("ahmedelsayad/java-app")
                }
            }
        }
    }
}
