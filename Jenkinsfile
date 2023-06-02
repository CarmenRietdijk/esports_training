pipeline {
    agent any
    environment {
        DOTNET_SDK_VERSION = '7.0'
        PATH = "${tool(name: 'dotnetOnJenkins', type: 'hudson.plugins.dotnet.DotNetToolInstallation').getHome()}:${env.PATH}"
    }
    stages {
        stage('Build') { 
            steps {
                sh '/opt/homebrew/bin/docker-compose -f docker-compose.yml down'
                sh '/opt/homebrew/bin/docker-compose -f docker-compose.yml up -d'
            }
        }
        stage('Test') { 
            steps {
                script {
                    def containerNames = ['esports_training-selenium-hub-1', 'esports_training-firefox-1', 'esports_training-chrome-1']
                    for (def containerName in containerNames) {
                        withDotNet{
                            dotnetTest(filter: 'testcategory=demo') 
                        }
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
