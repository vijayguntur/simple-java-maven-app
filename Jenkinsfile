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
                 
                File file = new File("out.txt")
                file.append("hello\n")
                file.append("second hello\r\n")
                //unstash 'app'
                //writeFile file: 'RunAssessment.txt', text: 'Working with files the Groovy way is easy.\r\n'
                //file.append("second line comes here\n")
                //sh './jenkins/scripts/deliver.sh'
            }
        }
    }
}
