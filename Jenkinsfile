pipeline {
    agent any
    
    parameters {
        choice(name: 'BUILD_CONFIG', choices: ['Release', 'Debug'], description: 'Build configuration')
    }
    
    stages {
        stage ('Checkout') {
            steps {
                cleanWs()
                bat "git clone https://github.com/Gamedev-Crafters/JenkinsDotNet.git ."
            }
        }
        
        stage ('Test') {
            steps {
                bat "dotnet test --configuration ${BUILD_CONFIG} --no-build --logger trx --results-directory TestResults"
            }
        }
        
        stage('Restore') {
            steps {
                bat "dotnet restore"
            }
        }
        
        stage('Build') {
            steps {
                bat "dotnet build --configuration ${BUILD_CONFIG} --no-restore"
            }
        }
        
        stage('Publish') {
            steps {
                bat """
                    dotnet publish --configuration ${BUILD_CONFIG} --no-build --output "Publish" --framework net6.0
                """
                archiveArtifacts artifacts: 'Publish/**/*', fingerprint: true
            }
        }
    }
}