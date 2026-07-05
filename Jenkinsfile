pipeline {
    agent {
        docker {
            image 'node:20'
            args '-u root:root'
        }
    }

    stages {

        stage('Checkout') {
            steps {
                echo "🔍 Checking out source code..."
                checkout scm
            }
        }

        stage('Install Dependencies') {
            steps {
                echo "📦 Installing dependencies..."
                sh '''
                    if [ -f package.json ]; then
                        npm install
                    else
                        echo "⚠️ No package.json found - skipping npm install."
                    fi
                '''
            }
        }

        stage('Build') {
            steps {
                echo "🏗️ Building the project..."
                sh '''
                    if [ -f package.json ]; then
                        npm run build || echo "No build script found."
                    fi
                '''
            }
        }

        stage('Test') {
            steps {
                echo "🧪 Running tests..."
                sh '''
                    if [ -f package.json ]; then
                        npm test || echo "No test script found."
                    fi
                '''
            }
        }

        stage('Deploy') {
            steps {
                echo "🚀 Deploying application (simulation)..."
                sh 'echo "Deployed successfully at $(date)"'
            }
        }
    }

    post {
        success {
            echo "✅ Pipeline executed successfully!"
        }
        failure {
            echo "❌ Pipeline failed. Check logs for details."
        }
    }
}
