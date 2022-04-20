pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                sh '''pwd
                    cd public
                    pwd
                    ls -la | grep Dock
                    docker build -t nginx-server:v2 .'''
            }
        }
        stage('Stop_older_instance') { 
            steps {
                sh 'docker stop jenkins-assignment2'
                sh 'sudo docker container ls -a | grep jenkins-assignment2 | cut -c -12 > ~/docker_jenkins_no_pipeline.txt'
                sh 'cat ~/docker_jenkins_no_pipeline.txt | xargs sudo docker container rm'
            }
        }
        stage('Deploy') { 
            steps {
                sh 'docker run --name jenkins-assignment2 -d -p 8082:80 nginx-server:v2'
            }
        }
    }
}
