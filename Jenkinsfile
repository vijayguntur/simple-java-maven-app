pipeline {
    agent { label 'master' }
    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
                bat 'echo %path%'
                stash includes: '**/target/*.jar', name: 'app'
            }
        }
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
            agent { label 'Javabuild' }
            steps {
                dir('..\..\')
                unstash 'app'
                //sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
