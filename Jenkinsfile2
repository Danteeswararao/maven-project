pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving....'
                    archiveArtifacts artifacts: '**/target/*.war' 
                }
            }
        }
        stage('Deploy to Stag') {
            steps {
                build job: 'deploy-to-tomcat-stg'
            }
        }
        stage('Deploy to Prod') {
            steps {
                timeout(time:5, unit:'DAYS'){
                    input message: 'Approve the Production Deployment?'
                }
                
                build job: 'deploy-tomcat-prod'
            }
            post {
                success {
                    echo 'Code Deployed to Production...'
                }
                failure {
                    echo 'Deployment Failed ...'
                }
            }
        }
    }
}
