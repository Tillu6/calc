pipeline {
    agent any

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/Tillu6/calc'
            }
        }

        stage('Build') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'xcodebuild -scheme CalculatorApp build' // For iOS
                    } else {
                        bat 'gradlew assembleDebug' // For Android
                    }
                }
            }
        }

        stage('Test') {
            steps {
                script {
                    if (isUnix()) {
                        sh 'xcodebuild test -scheme CalculatorApp' // For iOS
                    } else {
                        bat 'gradlew test' // For Android
                    }
                }
            }
        }

        stage('Code Quality Analysis') {
            steps {
                withSonarQubeEnv('SonarQube') {
                    script {
                        if (isUnix()) {
                            sh './gradlew sonarqube' // For Android
                        } else {
                            sh 'xcodebuild clean build' // For iOS with SonarQube support
                        }
                    }
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                script {
                    // Deployment steps (e.g., Docker, Firebase, TestFlight)
                }
            }
        }

        stage('Deploy to Production') {
            steps {
                script {
                    // Deployment steps for production
                }
            }
        }

        stage('Monitoring and Alerting') {
            steps {
                script {
                    // Set up monitoring and alerting (e.g., Datadog, New Relic)
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
