pipeline {
    agent { label 'master' }
    stages {
        stage('Build') {
            steps {
                bat 'mvn -B -DskipTests clean package'
                bat 'echo %path%'
                //stash includes: '**/target/*.jar', name: 'app'
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
            //agent { label 'Javabuild' }
            steps {
                 def ln = System.getProperty('line.separator')
                 writeFile file: 'RunAssessment.txt', text: 'Working with files the Groovy way is easy.'+ ln + 'second line' + ln + '#third line commnets'
                
                //unstash 'app'
                //writeFile file: 'RunAssessment.txt', text: 'Working with files the Groovy way is easy.'+ \\r\\n 'second line' + \\r\\n '#third line commnets'
                //sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
