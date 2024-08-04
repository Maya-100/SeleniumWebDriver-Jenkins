
pipeline {
    agent any

    stages{
        stage('Checkout code') {
            //checkout the repository
            steps {
                git branch: 'main', url: 'https://github.com/Maya-100/SeleniumWebDriver-Jenkins'
            }
        }
        // stage('Set up .Net Core') {
        //     //install .Net
        //     steps {
        //          sh '''
        //          echo Installing .Net SDK 6.0
        //         // NONINTERACTIVE=1 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
        //         // brew install --cask dotnet-sdk6-0-132
        //          '''
        //     } 
        // }
        stage('Restoring nuget packages') {
           //install dependencies
            steps {
                sh '/opt/homebrew/bin/dotnet restore SeleniumBasicExercise.sln'
            } 
        }
        stage('Build') {
            //build
            steps {
                sh '/opt/homebrew/bin/dotnet build SeleniumBasicExercise.sln --configuration Release'
            }
        }
        stage('Run Tests TestProject1') {
            //run test
            steps {
                sh '/opt/homebrew/bin/dotnet test TestProject1/TestProject1.csproj --logger "trx;LogFileName=TestResults.trx"'
            }
        }
        stage('Run Tests TestProject2') {
            //run test
            steps {
                sh '/opt/homebrew/bin/dotnet test TestProject2/TestProject2.csproj --logger "trx;LogFileName=TestResults.trx"'
            }
        }
        stage('Run Tests TestProject3') {
            //run test
            steps {
                sh '/opt/homebrew/bin/dotnet test TestProject3/TestProject3.csproj --logger "trx;LogFileName=TestResults.trx"'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/TestResults/*.trx', allowEmptyArchive: true
            step([
                $class: 'MSTestPublisher',
                testResultsFile: '**/TestResults/*.trx'
            ])
            
        }
    }
}

