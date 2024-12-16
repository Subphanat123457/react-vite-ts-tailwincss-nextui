pipeline {
    agent any
    
    environment {
        GITHUB_CREDENTIALS_ID = 'github-app-credentials' // ระบุ ID ของ GitHub App Credentials
        REPOSITORY_URL = 'https://github.com/username/repository-name.git'
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    doGenerateSubmoduleConfigurations: false,
                    extensions: [],
                    userRemoteConfigs: [[
                        url: "${REPOSITORY_URL}",
                        credentialsId: "${GITHUB_CREDENTIALS_ID}"
                    ]]
                ])
            }
        }

        stage('Build') {
            steps {
                echo 'Building the application...'
                sh './gradlew build' // ตัวอย่างคำสั่งสำหรับ Build (เปลี่ยนตามโปรเจกต์)
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh './gradlew test' // ตัวอย่างคำสั่งสำหรับการทดสอบ
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying application...'
                sh './scripts/deploy.sh' // เรียกใช้สคริปต์ Deploy (ถ้ามี)
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
        always {
            cleanWs() // ล้าง workspace
        }
    }
}
