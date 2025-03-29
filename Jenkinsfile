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
                        paramPublish: [
                            [
                                configName: 'e4b6ff5f-fdc7-4baa-b3cf-ecff8eeb090f', // Nombre de la configuración FTP en Jenkins
                                transfers: [
                                    [
                                        sourceFiles: '**/*.zip', // Archivos a transferir
                                        remoteDirectory: '/site/wwwroot', // Directorio remoto en Azure
                                        removePrefix: '',
                                        remoteDirectorySDF: false,
                                        flatten: false
                                    ]
                                ],
                                useWorkspaceInPromotion: false,
                                usePromotionTimestamp: false
                            ]
                        ]
                    )
            }
        }
    }
}
