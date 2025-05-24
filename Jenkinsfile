pipeline {
    agent {
        docker {
            image 'node:18' // Use Node.js 18 Docker image
            args '-v /var/run/docker.sock:/var/run/docker.sock' // Bind Docker socket
        }
    }

    environment {
        FRONTEND_DIR = 'client'
        BACKEND_DIR = 'server'
    }

    stages {
        stage('Checkout Code') {
            steps {
                checkout scm
            }
        }

        // stage('Install & Build Frontend') {
        //     steps {
        //         dir("${env.FRONTEND_DIR}") {
        //             sh 'npm install'
        //             sh 'npm run dev' // Build frontend for production
        //         }
        //     }
        // }

        stage('Install & Build Backend') {
            steps {
                dir("${env.BACKEND_DIR}") {
                    sh 'npm install'
                    sh 'npm run dev' // Build backend for production
                }
            }
        }

        // stage('Run Tests') {
        //     parallel {
        //         stage('Frontend Tests') {
        //             steps {
        //                 dir("${env.FRONTEND_DIR}") {
        //                     sh 'npm run test' // Run frontend tests
        //                 }
        //             }
        //         }
        //         stage('Backend Tests') {
        //             steps {
        //                 dir("${env.BACKEND_DIR}") {
        //                     sh 'npm run test' // Run backend tests
        //                 }
        //             }
        //         }
        //     }
        // }
    }

    post {
        success {
            echo '✅ Build and tests succeeded!'
        }
        failure {
            echo '❌ Build or tests failed. Check the console output for errors.'
        }
    }
}