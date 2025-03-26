pipeline {
    agent any
    stages {
        stage('Configurar Entorno Virtual') {
            steps {
                sh 'python3 -m venv venv'       
                sh 'source venv/bin/activate'   
                sh 'venv/bin/pip install --upgrade pip'  
                sh 'venv/bin/pip install -r requeriments.txt'  
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
