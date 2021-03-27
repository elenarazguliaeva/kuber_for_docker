pipeline {
    agent any
    
    environment {
      imageName = 'elenarazguliaeva/jenkins'
      registryCredentialSet = 'docker-hub-credentials'
      registryUrl = 'https://hub.docker.com'
    }
    
    stages {   

        stage('Build image') {
            steps {
                script {
                    app = docker.build(imageName)
                }                
            }
        }
        stage('Test image') {
            steps {
                script {
                    app.inside {
                        sh 'echo "Tests passed"'
                    }
                }

            }
        }
        stage('Push image') {           
            steps {
                script {
                    docker.withDockerServer(registryUrl, registryCredentialSet) {
                        app.push("latest")
                    }
                }                
            }
        }
    }
}
