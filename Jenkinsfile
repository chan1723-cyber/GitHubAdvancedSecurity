pipeline {
    agent any
    stages {
        stage('Instalar Dependencias') {
            steps {                
                sh 'python3 -m pip install --upgrade pip --break-system-packages'
                sh 'python3 -m pip install -r requeriments.txt --break-system-packages'
            }
        }
        stage('Ejecutar los tests') {
            steps {
               sh 'python3 app/validation.py'
            }
        }
        stage('Empaquetar') {
            steps {
                sh 'zip -r app.zip *'
            }
        }
        stage('Deploy') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'e4b6ff5f-fdc7-4baa-b3cf-ecff8eeb090f', usernameVariable: 'FTP_USER', passwordVariable: 'FTP_PASS')]) {
                    sh """
                    lftp -e "set ftp:ssl-allow no; mirror -R . /site/wwwroot; bye" -u $FTP_USER,$FTP_PASS ftps://waws-prod-yt1-083.ftp.azurewebsites.windows.net
                    """
                }
            }
        }
    }
}
