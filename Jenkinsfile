pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/santhosh-jadi/python.git'
            }
        }

        stage('Verify Python') {
            steps {
                bat 'python --version'
            }
        }

        stage('Install Dependencies') {
            steps {
                bat 'python -m pip install -r requirements.txt'
                bat 'python -m pip install pyinstaller'
            }
        }

        stage('Test') {
            steps {
                bat 'python -m unittest discover -v'
            }
        }

        stage('Package') {
            steps {
                bat 'python -m PyInstaller --onefile calculator.py'
            }
        }

        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'dist/*.exe',
                    fingerprint: true
            }
        }
    }

    post {
        success {
            echo 'Python CI/CD Successful'
        }
        failure {
            echo 'Python CI/CD Failed'
        }
    }
}
