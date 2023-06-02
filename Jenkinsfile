pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                sh '/opt/homebrew/bin/docker-compose -f docker-compose.yml down'
                sh '/opt/homebrew/bin/docker-compose -f docker-compose.yml up -d'
                sleep 30 
            }
        }
        stage('Test') { 
            steps {
                script {
                    def containerNames = ['esports_training-selenium-hub-1', 'esports_training-firefox-1', 'esports_training-chrome-1']
                    for (def containerName in containerNames) {
                        sh "/opt/homebrew/bin/docker-compose exec ${containerName} dotnet test --filter testcategory=demo" 
                    }
                }
            }
        }
        stage('Deploy') { 
            steps {
                sh '/opt/homebrew/bin/docker-compose -f docker-compose.yml down' 
            }
        }
    }
}
