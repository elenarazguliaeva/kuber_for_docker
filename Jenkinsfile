pipeline {
    agent any
    stages {
        def app
        stage('Clone repository') {
            steps {
                checkout scm
            }
        }
        stage('Build image') {
            steps {
                app = docker.build("elenarazguliaeva/jenkins")
            }
        }
        stage('Test image') {
            steps {
                app.inside {
                    sh 'echo "Tests passed"'
                }
            }
        }
        stage('Push image') {           
            steps {
                docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                     app.push("${env.BUILD_NUMBER}")
                     app.push("latest")
                }
            }
        }
    }
}
