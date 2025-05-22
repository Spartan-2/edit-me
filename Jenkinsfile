pipeline {
    agent any

    environment {
        FRONTEND_DIR = 'client'
        BACKEND_DIR = 'server'
        DOCKER_REGISTRY = 'your-dockerhub-username' // Replace with your DockerHub username
        FRONTEND_IMAGE = 'mern-frontend'
        BACKEND_IMAGE = 'mern-backend'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/Spartan-2/edit-me'
            }
        }

        stage('Install & Build Frontend') {
            steps {
                dir("${env.FRONTEND_DIR}") {
                    sh 'npm install'
                    // Use `npm run build` if it's a production build step
                    sh 'npm run dev'
                }
            }
        }

        stage('Install & Start Backend') {
            steps {
                dir("${env.BACKEND_DIR}") {
                    sh 'npm install'
                    sh 'npm run dev'
                }
            }
        }
    }

    post {
        success {
            echo '✅ Build and startup succeeded!'
        }
        failure {
            echo '❌ Build failed. Check the console output for errors.'
        }
    }
}
