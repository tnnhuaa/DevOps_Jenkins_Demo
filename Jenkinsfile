pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out code...'
                checkout scm
            }
        }
        
        stage('Setup') {
            steps {
                echo 'Setting up Python environment...'
                sh '''
                    python --version
                    python -m pip install --upgrade pip
                    python -m venv venv
                    . venv/bin/activate
                    pip install -r requirements.txt || echo "No requirements.txt found, skipping..."
                '''
            }
        }
        
        stage('Test') {
            steps {
                echo 'Running unit tests...'
                sh '''
                    . venv/bin/activate
                    python -m pytest test_baitap1.py -v --tb=short || python -m unittest test_baitap1 -v
                '''
            }
        }
    }
    
    post {
        always {
            echo 'Test stage completed'
        }
        success {
            echo 'All tests passed successfully!'
        }
        failure {
            echo 'Tests failed!'
        }
    }
}
