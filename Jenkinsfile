pipeline {
    
    agent any
    
    stages {
        stage ("checkout") {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/ashumesh/mydockerreponiraj.git']]])
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
                    
                    sh 'docker push ashwinimesh12345/ashwinirepo'
                }
            }
            
        }
        
        
        // Stopping the docker container for cleaner docker run
        
        stage ("Stop previos container"){
            steps {
                sh 'docker ps -f name=mypythonContainer -q | xargs --no-run-if-empty docker container stop'
                sh 'docker container ls -a -fname=mypythonContainer -q | xargs -r docker container rm'
            }
        }
        
        stage ("Docker run") {
            steps {
                script {
                    sh 'docker run -d -p 8096:5000  --rm --name mypythonContainer ashwinimesh12345/ashwinirepo'
                }
            }
        }
    }
}
