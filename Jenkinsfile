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
                sh 'screen -dmS banking_app bash -c "python3 run.py > banking_app.log 2>&1"'
                sleep 5
            }
        }
        stage('Verificar Screen') {
            steps {
                sh 'screen -ls'
            }
        }
        stage('Ver Logs de la Aplicación') {
            steps {
                sh 'sleep 5'  // Esperar un poco para que la app se inicie
                sh 'cat banking_app.log || echo "No hay logs aún"'
            }
        }
    }
}
