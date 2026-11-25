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
    }
}

