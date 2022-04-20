pipeline {
    agent any 
    stages {        
        stage('Build') { 
            steps {
                sh '''
                    cd public
                    echo '<p>' >> jenkinsassignment.html
                    echo $BUILD_ID >> jenkinsassignment.html
                    echo '</p>' >> jenkinsassignment.html
                    docker build -t nginx-server:v2 .'''
            }
        }
        stage('Stop previous test instance') { 
            steps {
                sh '''docker stop jenkins-assignment2-test
                    sudo docker container ls -a | grep jenkins-assignment2-test | cut -c -12 > ~/docker_jenkins_no_pipeline_test.txt
                    cat ~/docker_jenkins_no_pipeline_test.txt | xargs sudo docker container rm
                    exit'''
            }
        }
        stage('Deploy to test') { 
            steps {
                sh 'docker run --name jenkins-assignment2-test -d -p 8084:80 nginx-server:v2'
            }
        }
        stage('Smoke test') { 
            steps {
                sh 'curl localhost:8084/jenkinsassignment.html | grep $BUILD_ID'       
            }
        }
        stage('Manual approval') {
            agent none
            steps {
                input "Deploy to prod?"
            }
        }
        stage('Stop previous prod instance') { 
            steps {
                sh '''docker stop jenkins-assignment2
                    sudo docker container ls -a | grep jenkins-assignment2 | cut -c -12 > ~/docker_jenkins_no_pipeline.txt
                    sudo su
                    cat ~/docker_jenkins_no_pipeline.txt | xargs sudo docker container rm'''
            }
        }
        stage('Deploy to prod') { 
            steps {
                sh 'docker run --name jenkins-assignment2 -d -p 8082:80 nginx-server:v2'
            }
        }
    }
}
