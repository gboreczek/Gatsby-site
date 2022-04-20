pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                cd C:\ProgramData\Jenkins\.jenkins\workspace\JenkinsAssignment1.1\public
                docker build -t nginx-server:v1 .
                docker stop jenkins-assignment1 
            }
        }
        stage('Stop_older_instance') { 
            steps {
                docker stop jenkins-assignment1
                sh docker container ls -a | grep jenkins-assignment1 | cut -c -12 | docker container rm  
            }
        }
        stage('Deploy') { 
            steps {
                docker run --name jenkins-assignment1 -d -p 8081:80 nginx-server:v1
            }
        }
    }
}
