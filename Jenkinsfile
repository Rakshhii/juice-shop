pipeline {
    agent any
    
    environment {
        CXONE_API_KEY = credentials('eyJhbGciOiJIUzUxMiIsInR5cCIgOiAiSldUIiwia2lkIiA6ICIzNTM0MTE1MC0yNjFlLTRkZDctYmU0YS1kMzAzYmY4YzcwM2YifQ.eyJpYXQiOjE3NTg2NDA5OTYsImp0aSI6ImY5OWIwMWRmLWU5YWItNDU5Zi1iMDY0LWViOTc4NTFhZjk4ZSIsImlzcyI6Imh0dHBzOi8vaW5kLmlhbS5jaGVja21hcngubmV0L2F1dGgvcmVhbG1zL2N4X2luZF9pbnRlcm5hbF90ZXN0IiwiYXVkIjoiaHR0cHM6Ly9pbmQuaWFtLmNoZWNrbWFyeC5uZXQvYXV0aC9yZWFsbXMvY3hfaW5kX2ludGVybmFsX3Rlc3QiLCJzdWIiOiJjMzA2YTVhNi1jZTBlLTRkOTMtOTk5Ny00NTYzNzAzNDlkNzIiLCJ0eXAiOiJPZmZsaW5lIiwiYXpwIjoiYXN0LWFwcCIsInNpZCI6ImYyNjlkNmM5LWRjOGMtNDY2Yy04Nzg1LWQxOGYxZDQ4ZTRjZiIsInNjb3BlIjoicHJvZmlsZSBpYW0tYXBpIGdyb3VwcyByb2xlcyBlbWFpbCBhc3QtYXBpIG9mZmxpbmVfYWNjZXNzIn0.zUrzyVZU4QRRGWD2NolBcoG0a7w3huhJLlZCtmCGy8SJYZhW39c1igX1QXxAhPwhMLVuJccdZ9rbJzMrBfoZtg')  // Reference stored credentials
        CXONE_URL = 'https://ind.ast.checkmarx.net'  // Example API endpoint for CXOne
    }
    
    stages {
        stage('Checkout') {
            steps {
                // Checkout your source code from version control (GitHub, GitLab, etc.)
                git 'https://github.com/Rakshhii/juice-shop'
            }
        }
        
        stage('Build') {
            steps {
                // Execute build commands here (e.g., Maven, Gradle, npm)
                echo 'Building the project...'
            }
        }
        
        stage('Deploy to CXOne') {
            steps {
                script {
                    // Call CXOne API to deploy
                    def response = httpRequest(
                        acceptType: 'APPLICATION_JSON',
                        contentType: 'APPLICATION_JSON',
                        url: "${env.CXONE_URL}/deploy",
                        httpMode: 'POST',
                        requestBody: '{"apiKey": "' + env.CXONE_API_KEY + '", "application": "your-app"}'
                    )
                    echo "CXOne API Response: ${response}"
                }
            }
        }
        
        stage('Test') {
            steps {
                // Run your test cases (unit, integration, or end-to-end tests)
                echo 'Running tests...'
            }
        }
        
        stage('Clean Up') {
            steps {
                // Optional: clean up any resources if needed
                echo 'Cleaning up...'
            }
        }
    }
    
    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
