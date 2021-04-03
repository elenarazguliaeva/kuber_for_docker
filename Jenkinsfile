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
                    withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'USER', passwordVariable: 'PASSWORD')]) {

                        sh "docker login -u $USER -p $PASSWORD ${registryUrl}"
                        docker.withRegistry(registryUrl, registryCredentialSet) {
                            app.push()
                        }
                    }
                }
            }
        }
    }
}
