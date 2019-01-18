pipeline {
    agent any
    stages {
        stage {
            steps {
                sh 'mvn clean package'
            }
            post {
                success {
                    echo 'Now Archiving....'
                    archiveAritifacts artifacts: '**/target/*.war' 
                }
            }
        }
    }
}
