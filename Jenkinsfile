pipeline {
    agent {
        label 'slave1'
    }

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-amazon-corretto.x86_64'
        PATH = "${JAVA_HOME}/bin:${env.PATH}"
        Dockerhub_credentials = credentials('dockerhub_credentials')
    }

    stages {

        stage('SCM Checkout') {
            steps {
                echo "performing scm_checkout"

                git branch: 'master',
                    url: 'https://github.com/jayanth163/Microservice-Deployment-of-Java-Application-Using-CI-CD.git
'
            }
        }

        stage('Build the artifacts') {
            steps {
                echo "performing application build"

                sh 'mvn clean package'
            }
        }

        stage('Creating Docker image') {
            steps {
                echo "performing application image"
                sh 'docker image prune -af'
                sh 'docker build -t jayanth16316/banking_app:${BUILD_NUMBER} .'
                sh 'docker tag jayanth16316/banking_app:${BUILD_NUMBER} jayanth16316/banking_app:latest'
            }
        } 
        
        stage('Login to Docker Hub') {
            steps {
                sh 'echo $Dockerhub_credentials_PSW | docker login -u $Dockerhub_credentials_USR --password-stdin'
            }
        }

        stage('Publishing the image') {
            steps {
                echo "performing image publishing to container registry"

                sh 'docker push jayanth16316/banking_app:latest'
            }

            post {
                success {
                    mail(
                        bcc: '',
                        body: '''Hi,

This is to inform you that if you have received this mail, then CONGRATULATIONS!!

Your project is already complete.

Regards,
Jayanth
''',
                        cc: '',
                        from: '',
                        replyTo: '',
                        subject: 'Updates regarding Jenkins CI/CD project',
                        to: 'jayanth16316@outlook.com'
                    )
                }
            }
        }

        stage('Deploying to Kubernetes server') {
            steps {
                script {
                    sshPublisher(publishers: [sshPublisherDesc(configName: 'kubernetes_server', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'kubectl apply -f bankingdeploy.yaml', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '.', remoteDirectorySDF: false, removePrefix: '', sourceFiles: '*.yaml')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                }
            }
        }
    }
}


