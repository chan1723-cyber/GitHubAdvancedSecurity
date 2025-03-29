pipeline {
    agent any
    stages {
        stage('Clonar código') {
            steps {
                script {
                    checkout scm
                }
            }
        }
        stage('Ejecutar pruebas unitarias') {
            steps {
                sh 'python3 app/validation.py'
            }
        }
        stage('Ejecutar pruebas automatizadas') {
            steps {
                sh 'pip3 install selenium && python3 test_banking.py'
            }
        }
        stage('Construir imagen Docker') {
            steps {
                sh 'docker build -t mi_app .'
            }
        }
        stage('Ejecutar contenedor') {
            steps {
                sh 'docker run -d -p 5000:5000 --name mi_app_container mi_app'
            }
        }
        stage('Verificar contenedores') {
            steps {
                sh 'docker ps -a'
            }
        }
    }
}
