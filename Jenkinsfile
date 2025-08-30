pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/Pranesh-2005/jenkins-demo.git'
            }
        }

        stage('Install Dependencies') {
            steps {
                sh 'pip install -r requirements.txt'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'pytest'
            }
        }

        stage('Deploy to Render') {
            steps {
                withCredentials([string(credentialsId: 'RENDER_API_KEY', variable: 'RENDER_TOKEN')]) {
                    sh '''
                      curl -X POST "https://api.render.com/v1/services/<YOUR_SERVICE_ID>/deploys" \
                      -H "Authorization: Bearer $RENDER_TOKEN" \
                      -H "accept: application/json" \
                      -H "content-type: application/json"
                    '''
                }
            }
        }
    }
}
