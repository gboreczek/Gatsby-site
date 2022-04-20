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
        
        stage('Deploy') { 
            steps {
                sh 'docker run --name jenkins-assignment2 -d -p 8082:80 nginx-server:v2'
            }
        }
    }
}
