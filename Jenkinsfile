pipeline {
    agent any 
    stages {
        stage('Build') { 
            steps {
                sh '''
                    cd public
                    echo $BUILD_ID >> jenkinsassignment.html
                    docker build -t nginx-server:v2 .'''
            }
        }
        stage('Manual approval') {
            agent none
            steps {
                input "Deploy to prod?"
            }
        }
        stage('Stop_older_instance') { 
            steps {
                sh '''docker stop jenkins-assignment2
                    sudo docker container ls -a | grep jenkins-assignment2 | cut -c -12 > ~/docker_jenkins_no_pipeline.txt
                    cat ~/docker_jenkins_no_pipeline.txt | xargs sudo docker container rm'''
            }
        }
        stage('Deploy') { 
            steps {
                sh 'docker run --name jenkins-assignment2 -d -p 8082:80 nginx-server:v2'
            }
        }
    }
}
