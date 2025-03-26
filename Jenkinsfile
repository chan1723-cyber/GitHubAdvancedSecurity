pipeline {
    agent any
    stages {
        stage('Instalar Dependencias') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }
        stage('Ejecutar la Aplicación') {
            steps {
                sh 'python run.py &'
            }
        }
        stage('Exponer con Ngrok') {
            steps {
                sh 'ngrok http 5000 &'
                sleep 5
                sh 'curl -s http://localhost:4040/api/tunnels'
            }
        }
    }
}
