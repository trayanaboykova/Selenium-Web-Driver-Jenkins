pipeline {
    agent any

    stages {
        stage('Checkout the repository') {
            steps {
                checkout scm
            }
        }

        stage('Restore the project') {
            steps {
                bat 'dotnet restore'
            }
        }


        stage('Build the project') {
            steps {
                bat 'dotnet build'
            }
        }

        stage('Run tests') {
            parallel {
                stage('Project1 UI tests') {
                    steps {
                        bat 'dotnet test TestProject1 --no-build --verbosity normal'
                    }
                }
                stage('Project2 UI tests') {
                    steps {
                        bat 'dotnet test TestProject2 --no-build --verbosity normal'
                    }
                }
                stage('Project3 UI tests') {
                    steps {
                        bat 'dotnet test TestProject3 --no-build --verbosity normal'
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'Pipeline completed'
        }
        success {
            echo 'Build succeeded'
        }
        failure {
            echo 'Build failed'
        }
    }
}
