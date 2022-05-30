pipeline {
    
    agent any
    
    environment {
        registry = "817141239014.dkr.ecr.us-east-1.amazonaws.com/test-ecr"
    }
    
    stages {
        stage ("checkout") {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/nirajvishwakarma/mydockerrepo.git']]])
            }
        }
        
        stage ("Docker build") {
            steps {
                script {
                    dockerImage = docker.build registry
                }
            }
        }
        
        stage ("Docker upload") {
            steps {
                script {
                    sh 'aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 817141239014.dkr.ecr.us-east-1.amazonaws.com'
                    sh 'docker push 817141239014.dkr.ecr.us-east-1.amazonaws.com/test-ecr:latest'
                }
            }
            
        }
        
        
        // Stopping the docker container for cleaner docker run
        
        stage ("Stop previos container"){
            steps {
                sh 'docker ps -f name=mypythonContainer -q | xargs --no-run-if-empty docker conatainer stop'
                sh 'docker container ls -a -fname=mypythonContainer -q | xargs -r docker container rm'
            }
        }
        
        stage ("Docker run") {
            steps {
                script {
                    sh 'docker run -d -p 8096:5000  --rm --name mypythonContainer 817141239014.dkr.ecr.us-east-1.amazonaws.com/test-ecr:latest'
                }
            }
        }
    }
}
