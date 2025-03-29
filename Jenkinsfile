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
                        paramPublish: [[$class: 'BapFtpParamPublish']],  
                        publishers: [ftpPublisherPublisher(
                            configName: 'e4b6ff5f-fdc7-4baa-b3cf-ecff8eeb090f', 
                            transfers: [
                                sourceFiles: '**/*',  
                                remoteDirectory: '/site/wwwroot',  
                                removePrefix: '',
                                remoteDirectorySDF: false
                            ],
                            useWorkspaceInPromotion: false,
                            usePromotionTimestamp: false
                        )]
                    )
            }
        }
    }
}
