pipeline {
    agent any

    tools {
        maven '3'
    }

    options {
        skipStagesAfterUnstable()
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -v'
                sh 'mvn clean verify'
                sh 'mvn -B -DskipTests clean package' 
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver'){
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}