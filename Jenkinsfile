pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Récupérer le code depuis GitHub
                checkout([$class: 'GitSCM', branches: [[name: 'master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[url: 'https://github.com/emnaboukhris/dockerDevops2']]])
            }
        }
        stage('Build Docker Image') {
            steps {
                // Construire l'image Docker
                sh 'docker build -t item_service_image .'
            }
        }
        stage('Push to Docker Hub') {
            steps {
                // Se connecter à Docker Hub
                withCredentials([usernamePassword(credentialsId: 'docker-hub-credentials', usernameVariable: 'DOCKER_HUB_USERNAME', passwordVariable: 'DOCKER_HUB_PASSWORD')]) {
                    sh 'docker login -u $DOCKER_HUB_USERNAME -p $DOCKER_HUB_PASSWORD'
                }
                // Pousser l'image vers Docker Hub
                sh 'docker push mon-app'
            }
        }
    }
}
