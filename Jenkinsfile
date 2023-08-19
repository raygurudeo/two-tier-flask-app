pipeline {
    agent prod
    stages {
        stage("Prepare") {
            steps {
                git url: "https://github.com/raygurudeo/two-tier-flask-app.git", branch: "master"
            }
        }
        stage("Build & Test") {
            steps {
                echo "Code Built And Tested"
            }
        }
        stage("Push To Repository") {
            steps {
                echo "Image Pushed To Repository"
            }
        }
        stage("Deploy") {
            steps {
                echo "Application Deployed"
            }
        }
    }
}