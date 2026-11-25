pipeline {
    agent any

    tools {
        nodejs 'node18' 
    }

    environment {
        AWS_DEFAULT_REGION = 'us-east-1'
        S3_BUCKET          = 'sujith-s3-2026 '
    }

    stages {
        stage('Clone frontend repo') {
            steps {
                git url: 'https://github.com/sujith509/abc-frontend.git',
                    branch: 'main',
                    credentialsId: 'git-cred'
            }
        }
        stage('Install & build') {
            steps {
                sh '''
                npm ci
                npm run build
                '''
            }
        }
        stage('Deploy to S3') {
            steps {
                withAWS(credentials: 'aws-credssiva', region: 'ca-central-1') {
                    sh '''
                    echo "Uploading to S3"
                    aws s3 sync build/ "s3://${S3_BUCKET}" --delete
                    '''
                }
            }
        }
    }
}
