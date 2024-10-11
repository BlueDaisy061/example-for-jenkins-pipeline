pipeline {
    agent any
    tools { nodejs "nodejs"}
    stages {
        stage("Prepare") {
            steps {
                script {
                    env.GIT_SHOT = sh(script: "git rev-parse --short HEAD", returnStdout: true).trim()
                    currentBuild.displayName = "#${env.BUILD_NUMBER}: ${env.GIT_SHOT}"
                }
            }
        }
        stage("Build") {
            steps {
                script {
                    sh(
                        label: "Install npm dependencies",
                        script: "npm install"
                    )
                    sh(
                        label: "Run buil",
                        script: "npm run build"
                    )
                }
            }
        }
        stage("Unit test") {
            steps {
                script {
                    sh(
                        label: "Run unit tests",
                        script: "npm test"
                    )
                }
            }
        }
    }
    post {
        always {
            cleanWs()  // Clean workspace after each build
        }
    }
}