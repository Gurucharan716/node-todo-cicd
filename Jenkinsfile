pipeline {
    agent {label "dev-agent"}
    stages {
        stage("code clone") {
            steps {
                git url: "https://github.com/Gurucharan716/node-todo-cicd.git", branch: "master"
            }
        }
          stage("Build and Test") {
            steps {
                sh "docker build . -t gurucharan22/node-todo-app-new-cicd:latest"
            }
        }
           stage("Docker login and push image") {
            steps {
                echo "logging in docker hub and pushing image"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPassword",usernameVariable:"dockerHubUser")]) {
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                    sh "docker push gurucharan22/node-todo-app-new-cicd:latest"
                }
            }
        }
          stage("Deploy") {
            steps {
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
