pipeline {
    agent any
    stages {
        stage('Instalar Dependencias') {
            steps {                
                sh 'python3 -m pip install --upgrade pip --break-system-packages'
                sh 'python3 -m pip install -r requeriments.txt --break-system-packages'
            }
        }
        stage('Ejecutar la Aplicación') {
            steps {
                sh 'screen -dmS banking_app python run.py'
                sleep 5
            }
        }
    }
}
