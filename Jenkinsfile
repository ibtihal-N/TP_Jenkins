pipeline {
    environment {
        registry = "ibtihal12/tp_jenkins"   // Nom de l'image Docker
        registryCredential = 'dockerhub'    // Identifiants Docker Hub
        dockerImage = ''                    // Variable pour stocker l'image
    }
    agent any
    stages {
        stage('Cloning Git') {
            steps {
                git 'https://github.com/ibtihal-N/TP_Jenkins.git'  // URL du dépôt GitHub
            }
        }
        stage('Building image') {
            steps {
                script {
                    dockerImage = docker.build("${registry}:$BUILD_NUMBER")  // Construction de l'image Docker
                }
            }
        }
        stage('Test image') {
            steps {
                script {
                    echo "Tests passed"
                    // Ajoute ici des tests pour vérifier l'image si nécessaire
                }
            }
        }
        stage('Publish Image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push()  // Publication de l'image sur Docker Hub
                    }
                }
            }
        }
        stage('Deploy Image') {   // Nouveau stage pour déploiement
            steps {
                script {
                    // Lancer un conteneur à partir de l'image Docker construite et publiée
                    sh """
                    docker run -d --name my_container -p 8081:80 ${registry}:$BUILD_NUMBER
                    """
                }
            }
        }
    }
}
