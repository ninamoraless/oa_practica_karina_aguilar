pipeline {
    agent any

    options {
        timestamps()
    }

    stages {
        stage('Checkout') {
            steps {
                echo 'Obteniendo el código desde el repositorio Git...'
                checkout scm
            }
        }

        stage('Detener ambiente') {
            steps {
                echo 'Deteniendo contenedores existentes...'
                sh 'docker compose down'
            }
        }

        stage('Desplegar ambiente') {
            steps {
                echo 'Levantando WordPress y MySQL...'
                sh 'docker compose up -d'
            }
        }

        stage('Verificar despliegue') {
            steps {
                echo 'Verificando contenedores en ejecución...'
                sh 'docker ps'
                sh 'docker network ls'
                sh 'docker volume ls'
            }
        }
    }

    post {
        success {
            echo 'Despliegue completado. WordPress disponible en http://localhost:8000'
        }
        failure {
            echo 'El despliegue falló. Revise los logs del pipeline.'
        }
    }
}
