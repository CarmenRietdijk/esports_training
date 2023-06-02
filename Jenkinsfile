pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                sh '/opt/homebrew/bin/docker-compose -f docker-compose.yml down'
                sh '/opt/homebrew/bin/docker-compose -f docker-compose.yml up -d' 
            }
        }
        stage('Test') { 
            steps {
                sh "dotnet test --filter testcategory=demo" 
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
