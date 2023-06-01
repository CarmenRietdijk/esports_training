pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                sh '/opt/homebrew/bin/docker-compose -f docker-compose up -d' 
            }
        }
        stage('Test') { 
            steps {
                script {
                    def containerNames = ['esports-selenium-hub-1', 'esports-firefox-1', 'esports-chrome-1']
                    for (def containerName in containerNames) {
                        sh "docker-compose exec ${containerName} dotnet test --filter testcategory=demo" 
                    }
                }
            }
        }
        stage('Deploy') { 
            steps {
                sh 'docker-compose down' 
            }
        }
    }
}