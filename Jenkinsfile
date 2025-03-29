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
                        alwaysPublishFromMaster: false,
                        continueOnError: false,
                        failOnError: true,
                        masterNodeName: '',
                        paramPublish: [[$class: 'BapFtpParamPublish']],  // 📌 Configuración corregida
                        publishers: [ftpPublisherPublisher(
                            configName: 'AzureWebAppFTP',  // 📌 Nombre de la credencial de FTP en Jenkins
                            transfers: [ftpPublisherTransfer(
                                sourceFiles: '**/*',  // 📌 Subir todos los archivos del workspace
                                remoteDirectory: '/site/wwwroot',  // 📌 Directorio donde Azure Web App aloja los archivos
                                removePrefix: '',
                                remoteDirectorySDF: false
                            )],
                            useWorkspaceInPromotion: false,
                            usePromotionTimestamp: false
                        )]
                    )
            }
        }
    }
}
