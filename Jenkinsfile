@Library("Shared") _
pipeline {
    agent {label "vinod"}
    
    stages {
        
        stage("Hello"){
            steps{
                script{
                    hello()
                }
            }
        }
        stage ("Code"){
            steps{
                 script {
                   clone("https://github.com/Sudoharry/node-todo-cicd.git","master")

                 }
                
            }
        }
        
        stage ("Build"){
            steps {
               script{
                  docker_build("notes-app", "latest", "harendrabarot")
               }
            }
        }
        
        stage ("Test"){
            steps {
                echo "This is for testing the code"
             
           }
        }
        
        stage("Push To Dockerhub"){
            steps {
                script {
                    docker_push("notes-app", "latest", "harendrabarot" )
                }
                
            }
            
        }
        stage ("Deploy"){
            steps {
                echo "Stopping existing containers (if any)"
                sh "docker ps -q --filter 'name=notes-app' | xargs --no-run-if-empty docker stop"
                sh "docker ps -aq --filter 'name=notes-app' | xargs --no-run-if-empty docker rm"
        
                echo "Deploying the application"
                sh "docker run -d --name notes-app -p 8000:8000 notes-app:latest"
                }
        }
    }
}
