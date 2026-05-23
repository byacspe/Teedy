pipeline {
    agent any

    tools {
        maven 'Maven3'
        jdk 'JDK21'
    }

    stages {

        stage('Build') {
            steps {
                bat 'mvn clean install -DskipTests -U'
            }
        }

        stage('PMD Check') {
            steps {
                bat 'mvn clean install pmd:pmd -DskipTests -U'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('JavaDoc') {
            steps {
                bat 'mvn javadoc:javadoc'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package'
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: 'target/*.jar'
        }
    }
}