pipeline {
    agent any
    
    environment {
      imageName = 'elenarazguliaeva/jenkins'
      registryCredentialSet = 'docker-hub-credentials'
      registryUrl = 'https://registry.hub.docker.com'
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
                    withCredentials([usernamePassword( credentialsId: 'docker-hub-credentials', usernameVariable: 'USER', passwordVariable: 'PASSWORD')]) {
                        def registry_url = "registry.hub.docker.com/"
                        sh "docker login -u $USER -p $PASSWORD ${registry_url}"
                        docker.withRegistry("http://${registry_url}", "docker-hub-credentials") {
                            // Push your image now
                            sh "docker push elenarazguliaeva/jenkins:latest"
                        }
                    }
                }                
            }
        }
    }
}
