pipeline {
    agent any

    tools {
        maven 'Maven3'
        jdk 'JDK11'
    }

    stages {

        stage('Checkout') {
            steps {
                git 'https://github.com/sustech-cs304/Teedy.git'
            }
        }

        stage('Compile') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('PMD Check') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Generate JavaDoc') {
            steps {
                sh 'mvn javadoc:javadoc'
            }
        }
    }

    post {
        always {
            junit 'target/surefire-reports/*.xml'
            archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
            archiveArtifacts artifacts: 'target/site/**/*.*', fingerprint: true
        }
    }
}