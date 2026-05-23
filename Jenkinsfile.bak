pipeline {
    agent any

    tools {
        maven 'Maven3'
        jdk 'JDK17'
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/sustech-cs304/Teedy.git'
            }
        }

        stage('Compile') {
            steps {
                bat 'mvn clean compile'
            }
        }

        stage('PMD Check') {
            steps {
                bat 'mvn pmd:pmd'
            }
        }

        stage('Test') {
            steps {
                catchError(buildResult: 'SUCCESS', stageResult: 'UNSTABLE') {
                    bat 'mvn test'
                }
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package -DskipTests'
            }
        }

        stage('Generate JavaDoc') {
            steps {
                bat 'mvn javadoc:javadoc -DskipTests'
            }
        }
    }

    post {
        always {

            junit allowEmptyResults: true,
                   testResults: '**/target/surefire-reports/*.xml'

            archiveArtifacts artifacts: '**/target/*.jar',
                             fingerprint: true

            archiveArtifacts artifacts: '**/target/site/**/*.*',
                             fingerprint: true
        }
    }
}