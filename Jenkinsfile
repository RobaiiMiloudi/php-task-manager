pipeline {
    agent any

    options {
        skipDefaultCheckout()
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
                echo "Checked out ${env.BRANCH_NAME}"
            }
        }
        stage('Gitleaks') {
            steps {
                sh 'gitleaks git --log-opts=HEAD --redact=100 --exit-code=1 .'
            }
        }
        stage('SonarQube Analysis and Quality Gate') {
            when {
                branch 'dev'
            }
            steps {
                script {
                    def scannerHome = tool 'SonarScanner'
                    withSonarQubeEnv('SonarQube') {
                        withEnv(["PATH+SONAR=${scannerHome}/bin"]) {
                            sh 'sonar-scanner -Dsonar.qualitygate.wait=true -Dsonar.qualitygate.timeout=300'
                        }
                    }
                }
            }
        }        
    }
}
