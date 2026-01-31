// Create for me jenkins file to run unit test with Pyhton in file test_baitap1.py
// including create envỉonment and run test
pipeline {
    agent any

    stages {
        stage('Setup Python Environment') {
            steps {
                // Create a virtual environment
                sh 'python3 -m venv venv'
                
                // Activate the virtual environment and install dependencies
                sh '''
                    . venv/bin/activate
                    curl https://bootstrap.pypa.io/get-pip.py | python3
                    pip install --upgrade pip
                    pip install -r requirements.txt || echo "No requirements.txt found, skipping..."
                '''
            }
        }

        stage('Run Unit Tests') {
            steps {
                // Activate the virtual environment and run tests
                sh '''
                    . venv/bin/activate
                    python3 -m unittest discover -s . -p "test_baitap1.py"
                '''
            }
        }
    }

    post {
        always {
            // Clean up the virtual environment
            sh 'rm -rf venv'
        }
    }
}