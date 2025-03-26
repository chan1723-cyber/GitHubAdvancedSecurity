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
                sh 'tmux new-session -d -s banking_app "python3 run.py"'
                sleep 5
            }
        }
        stage('Verificar Screen') {
            steps {
                sh 'tmux list-sessions'            }
        }

    }
}
