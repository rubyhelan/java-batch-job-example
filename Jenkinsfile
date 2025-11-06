pipeline {
    agent any
    tools {
        jdk 'JDK17'
        maven 'Maven3'
    }
    stages {
        stage('Checkout') {
            steps{
            git url:'https://github.com/rubyhelan/java-batch-job-example.git',branch:'rubyhelan:feature/jenkin_02'
            }
        }
        stage('Build') {
            // write your logic here
               steps{
            bat 'mvn clean install'
            }
        }
        stage('Run Application') {
            // write your logic here
               steps{
            bat 'start /B java -jar target\\java-batch-job-example.jar'
            }
        }
        stage('Test') {
            // write your logic here
            steps{
            bat 'mvn install test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        stage('Post Build Notification') {
            // write your logic here
    }
    }

     post{
      success{
            echo 'Pipeline executed successfully'
            }
     failure{
            echo 'pipeline failed'
                }
            }
}
