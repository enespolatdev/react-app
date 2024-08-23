pipeline {
        agent {
            docker {
                image 'node:16-buster-slim'
                args '-p 3000:3000'
            }
        }
        stages {
            stage('Build') {
                steps {
                    sh 'npm install'
                }
            }
            stage('Test') {
                steps {
                    sh 'chmod +rx ./jenkins/scripts/*.sh'
                    sh './jenkins/scripts/test.sh'
                }
            }
            stage('Manual Approval') { 
                steps {
                    sh './jenkins/scripts/deliver.sh' 
                    input message: 'Dağıtım aşamasına geçilsin mi? (Devam etmek için "Devam Et"e tıklayın)'  
                }
            }
            stage('Deploy') { 
                steps {
                    sh './jenkins/scripts/deliver.sh' 
                    input message: 'React Uygulamasını kullanmayı bitirdiniz mi? (Sonlandırmak için "Devam Et"i tıklayın)'
                    sh './jenkins/scripts/kill.sh' 
                }
            }
        }
    }
