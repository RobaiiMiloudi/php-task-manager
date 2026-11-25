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
    }

}
