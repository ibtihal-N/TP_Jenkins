pipeline {
    environment {
        registry = "ibtihal12/tp_jenkins"
        registryCredential = 'dockerhub'
        dockerImage = ''
    }
    agent any
    stages {
        stage('Cloning Git') {
            steps {
                git 'https://github.com/ibtihal-N/TP_Jenkins.git'
            }
        }
        stage('Building image') {
            steps {
                script {
                    dockerImage = docker.build("${registry}:$BUILD_NUMBER")
                }
            }
        }
        stage('Test image') {
            steps {
                script {
                    echo "Tests passed"
                    // Ajoute ici des commandes pour tester l'image si nécessaire
                }
            }
        }
        stage('Publish Image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()
                    }
                }
            }
        }
    }
}
