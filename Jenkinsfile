pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Code checked out from GitHub'
                // Jenkins does this automatically when using
                // "Pipeline script from SCM"
            }
        }

        stage('Setup') {
            steps {
                echo 'Installing dependencies...'
                sh '''
    python3 -m venv venv
    ./venv/bin/pip install pytest
'''

            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'pytest -v test_calculator.py'
            }
        }

        stage('Run App') {
            steps {
                echo 'Running the app...'
                sh 'python3 calculator.py'
            }
        }
    }

    post {
        success {
            echo 'Build succeeded!'
        }
        failure {
            echo 'Build failed. Check the logs above.'
        }
    }
}
