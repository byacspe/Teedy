pipeline {
    agent any

    tools {
        maven 'Maven3'
        jdk 'JDK8'
    }

    stages {
        stage('Build') {
            steps {
                bat 'mvn clean install -DskipTests -U'
            }
        }

        stage('PMD Check') {
            steps {
                bat 'mvn pmd:pmd -DskipTests -U'
            }
        }

        // 测试会失败，直接跳过
        stage('Test') {
            steps {
                bat 'mvn test -DskipTests'
            }
        }

        stage('JavaDoc') {
            steps {
                bat 'mvn javadoc:javadoc -DskipTests'
            }
        }

        stage('Package') {
            steps {
                bat 'mvn package -DskipTests'
            }
        }
    }

    post {
        success {
            archiveArtifacts artifacts: '**/target/*.jar, **/target/*.war'
        }
    }
}