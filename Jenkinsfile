pipeline {
    agent { label 'Javabuild' }
    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
                bat 'echo %path%'
            }
        }
        agent { label 'master' }
        stage('Test') {
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
            steps {
                sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
