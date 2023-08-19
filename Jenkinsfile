pipeline {
    agent { label 'prod' }
    stages {
        stage("Prepare") {
            steps {
                git url: "https://github.com/raygurudeo/two-tier-flask-app.git", branch: "master"
            }
        }
        stage("Build & Test") {
            steps {
                sh "docker build . --rm -t two-tier-flask-app:latest"
                echo "Code Built And Tested"
            }
        }
        stage("Push To Repository") {
            steps {
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                    sh "docker tag two-tier-flask-app:latest ${env.dockerHubUser}/two-tier-flask-app:latest"
                    sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                    sh "docker push ${env.dockerHubUser}/two-tier-flask-app:latest"
                    echo "Image pushed to Dockerhub"
                }
            }
        }
        stage("Deploy") {
            steps {
                sh "docker-compose down && docker-compose up -d"
                echo "Application Deployed"
            }
        }
    }
}