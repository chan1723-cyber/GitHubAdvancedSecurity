pipeline {
    agent any
    stages {
        stage('Instalar Dependencias') {
            steps {                
                sh 'python3 -m pip install --upgrade pip'
                sh 'python3 -m pip install -r requeriments.txt --break-system-packages'
            }
        }
        stage('Ejecutar la Aplicación') {
            steps {
                sh 'python3 run.py &'
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
