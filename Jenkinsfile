pipeline {
    agent any
    tools {
        jdk 'JDK17'
        maven 'Maven3'
    }
    environment{
    EMAIL_RECIPIENTS:"rubyhelan@gmail.com"
    }
    stages {
        stage('Checkout') {
            steps{
            git url:'https://github.com/rubyhelan/java-batch-job-example.git',branch:'rubyhelan:feature/jenkin_03'
            }
        }
        stage('Build') {
            // write your logic here
               steps{
                   echo 'Building the project'
            bat 'mvn clean install'
            }
        }
        stage('Run Application') {
            // write your logic here
               steps{
            bat 'start /B java -jar target\\java-standalone-application.jar'
            }
        }
        stage('Test') {
            // write your logic here
            steps{
                echo 'Running tests'
            bat 'exit /b 1'
            }
            post {
                failure {
                   echo 'Tests failed.Sending email notification'
                   emailext (
                       subject: "Jenkins failure: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                       body:"""
                       <p>Hi Ruby</p>
                        <p>The test stage failed for Jenkins job <b>${env.JOB_NAME} </b> build #<b>${env.BUILD_NUMBER} </b>.</p>
                       <p>Check the console output at ${env.BUILD_URL}</p>
                           <p>Regards,<br></p>
                       """,
                      to: "${env.EMAIL_RECIPIENTS}",
                      mimeType:'text/html'
                )
            }
        }
        post{
      always{
            echo 'Pipeline executed successfully'
            }
    }

     
}
