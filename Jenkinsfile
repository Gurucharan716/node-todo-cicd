pipeline {
    agent {label "dev-agent"}
    stages {
        stage("code"){
            steps {
                git url: "https://github.com/Gurucharan716/node-todo-cicd.git", branch:"master"
            }
        }
         stage("Buils and Test"){
            steps {
                sh "docker build . -t gurucharan22/node-todo-app-cicd:latest"
            }
        }
         stage("Login and Image"){
            steps {
                echo "logging into docker hub and image"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPassword",usernameVariable:"dockerHubUser")]) {
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh "docker push gurucharan22/node-todo-app-cicd:latest"
                }
            }
        }
         stage("Deploying"){
            steps {
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
