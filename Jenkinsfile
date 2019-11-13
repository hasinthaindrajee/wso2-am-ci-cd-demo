pipeline {
    agent any
    environment {
        CI = 'true'
        API = './SwaggerPetstore'
    }
    stages {
        stage('Setup APIM Environments'){
            steps{
                withCredentials([usernamePassword(credentialsId: 'apim', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh './config.sh'
                }
            }
        }
        stage('Deploy to Test') {
            environment{
                ENV = 'test'
                RETRY = '80'
            }
            steps {
                echo 'Deploying to Test'
                sh '/Users/hasinthaindrajee/Downloads/apimcli/apimcli import-api -f $API -e $ENV -k --preserve-provider=false --update --verbose'
            }
        }
        stage('Deploy to Production') {
            environment{
                ENV = 'prod'
                RETRY = '60'
            }
            steps {
                echo 'Deploying to Production'
                sh '/Users/hasinthaindrajee/Downloads/apimcli/apimcli import-api -f $API -e $ENV -k --preserve-provider=false --update --verbose'
            }
        }
    }
}
