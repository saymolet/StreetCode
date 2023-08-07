pipeline {
    agent { 
        label 'stage' 
    }
    stages {
        stage('Restore Dependencies') {
            steps {
                sh 'dotnet restore ./Streetcode/Streetcode.sln'
            }
        }
        stage('Build') {
            steps {
                sh 'dotnet build ./Streetcode/Streetcode.sln --configuration Release --no-restore'
            }
        }
        stage('Test') {
            steps {
                sh 'dotnet test ./Streetcode/Streetcode.XUnitTest/Streetcode.XUnitTest.csproj --configuration Release --no-build --verbosity normal --collect:"XPlat Code Coverage" --results-directory ./coverage /p:CollectCoverage=true /p:CoverletOutputFormat=opencover /p:CoverletOutput=./coverage/coverage.xml'
            }
        }
        stage('Docker build') {
            steps {
                script {
                    Date date = new Date()
                    env.DATETAG = date.format("HH-dd-MM-yy", TimeZone.getTimeZone('GMT+3'))
                    sh "docker build -t streetcode/streetcode:${env.DATETAG} ."
                }
            }
        }
    }
}
