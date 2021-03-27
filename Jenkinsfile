pipeline {
    agent any
    
    environment {
      imageName = 'elenarazguliaeva/jenkins'
      registryCredentialSet = 'docker-hub-credentials'
      registryUrl = 'https://registry-1.docker.io/v2/'
    }
    
    stages {   

        stage('Build image') {
            steps {
                script {
                    app = docker.build(imageName)
                }                
            }
        }       
        stage('Push image') {           
            steps {
                script {
                    docker.withRegistry(registryUrl, registryCredentialSet) {
                        app.push()
                    }
                }                
            }
        }
    }
}
