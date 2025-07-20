pipeline {
    agent any
    
    stages {
        stage ('Checkout') {
            steps {
                cleanWs()
                bat "git clone https://github.com/Gamedev-Crafters/JenkinsDotNet.git ."
            }
        }
        
        stage ('Test') {
            steps {
                bat "dotnet test --configuration Release --logger trx --results-directory TestResults"
            }
        }
    }
}