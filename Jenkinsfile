pipeline {
    agent any

    environment {
        FRONTEND_DIR = 'client'
        BACKEND_DIR = 'server'
        DOCKER_REGISTRY = 'your-dockerhub-username'  // Change this
        FRONTEND_IMAGE = 'mern-frontend'
        BACKEND_IMAGE = 'mern-backend'
    }

    stages {
        stage('Checkout Code') {
            steps {
                git url: 'https://github.com/Spartan-2/edit-me'  // Replace with your repo
            }
        }

        stage("Install Dependencies"){
            steps{
                sh 'npm install'
            }
        }

        stage('Install & Build Frontend') {
            steps {
                dir("${env.FRONTEND_DIR}") {
                    sh 'npm install'
                    sh 'npm run dev'
                }
            }
        }

        stage('Install & Test Backend') {
            steps {
                dir("${env.BACKEND_DIR}") {
                    sh 'npm install'
                    sh 'npm run dev'
                }
            }
        }

    post {
        success {
            echo 'Build and Dockerization succeeded!'
        }
        failure {
            echo 'Build failed. Check logs for errors.'
        }
    }
}
