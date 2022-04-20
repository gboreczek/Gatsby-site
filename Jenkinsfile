pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                sh 'pwd'
                sh 'cd public'
                sh 'docker build -t nginx-server:v1 .'
            }
        }
        stage('Stop_older_instance') { 
            steps {
                sh 'docker stop jenkins-assignment1'
                sh 'sudo docker container ls -a | grep jenkins-assignment1 | cut -c -12 > ~/docker_jenkins_no_pipeline.txt'
                sh 'cat ~/docker_jenkins_no_pipeline.txt | xargs sudo docker container rm'
            }
        }
        stage('Deploy') { 
            steps {
                sh 'docker run --name jenkins-assignment1 -d -p 8081:80 nginx-server:v1'
            }
        }
    }
}
