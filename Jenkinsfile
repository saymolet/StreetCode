pipeline {
    agent { 
        label 'stage' 
    }
    stages {
        stage('Test') {
            steps {
                sh 'pwd'
                sh 'echo $DB_CONNECTION_STRING'
            }
        }
    }
}
