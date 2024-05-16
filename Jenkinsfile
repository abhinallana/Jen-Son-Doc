pipeline {
    agent any

    stages {
        stage('Checkout From Git') {
            steps {
                git branch: 'main', url: 'https://github.com/abhinallana/Jen-Son-Doc.git'
                echo 'Checkout from Repo'
            }
        }

        stage('SonarQube Analysis') {
            steps{
                script{
                    def scannerHome = tool 'SonarScanner';
                    withSonarQubeEnv() {
                        sh "${scannerHome}/bin/sonar-scanner"
                        echo "Successfully Scanned Vulnerabilities"
                    }
                }
            }
        }

        stage("Docker Build"){
            steps{
                script{
                sh 'docker --version'
                sh 'docker build -t fewebsite . '
                sh 'docker run -d -p 8085:80 --name=onixwebsite fewebsite'
            }
                
            }
        }
    }
}