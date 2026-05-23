pipeline {
    agent any

    tools {
        jdk 'JDK8'
        maven 'Maven'
    }

    stages {

        stage('Build') {
            steps {
                bat 'java -version'
                bat 'mvn -version'
                bat 'mvn clean install -DskipTests -U'
            }
        }

        stage('PMD Check') {
            steps {
                bat 'mvn pmd:pmd'
            }
        }

        stage('Test') {
            steps {
                bat 'mvn test'
            }
        }

        stage('JavaDoc') {
            steps {
                bat 'mvn javadoc:javadoc -Dmaven.javadoc.failOnError=false'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package -DskipTests'
            }
        }
    }
}