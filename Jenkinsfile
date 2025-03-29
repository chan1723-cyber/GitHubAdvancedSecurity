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
        stage('Subir a Azure por FTP') {
            steps {
                ftpPublisher(
                    publishers: [ftpPublisherPublisher(
                        configName: 'AzureWebAppFTP',
                        transfers: [ftpPublisherTransfer(
                            sourceFiles: 'app.zip',
                            remoteDirectory: '/site/wwwroot',
                            removePrefix: ''
                        )],
                        useWorkspaceInPromotion: false,
                        usePromotionTimestamp: false
                    )]
                )
            }

    }
}
