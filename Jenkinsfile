pipeline {
    agent none
    stages {
        stage('Build') {
            agent { label 'Javabuild' }
            steps {
                bat 'mvn -B -DskipTests clean package'
                bat 'echo %path%'
            }
        }
        stage('Test') {
            agent { label 'master' }
            steps {
                bat 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Deliver') {
            agent { label 'Javabuild' }
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
