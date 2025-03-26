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
                sh 'screen -dmS banking_app bash -c "python3 run.py"'
                sleep 5
            }
        }
        stage('Verificar Screen') {
            steps {
                sh 'screen -ls'
            }
        }
    }
}
