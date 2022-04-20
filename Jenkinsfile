pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                cd public
                docker build -t nginx-server:v1 .
            }
        }
        stage('Stop_older_instance') { 
            steps {
                docker stop jenkins-assignment1 
                sudo docker container ls -a | grep jenkins-assignment1 | cut -c -12 > ~/docker_jenkins_no.txt
                cat ~/docker_jenkins_no.txt | xargs sudo docker container rm 
            }
        }
        stage('Deploy') { 
            steps {
                docker run --name jenkins-assignment1 -d -p 8081:80 nginx-server:v1
            }
        }
    }
}
