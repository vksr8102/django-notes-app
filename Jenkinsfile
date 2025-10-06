@Library("Shared") _

pipeline {
    agent { label "vikash" }

    stages {
        stage("Hello") {
            steps {
                script {
                    hello()
                }
            }
        }

        stage("Code") {
            steps {
                echo "Code cloning started"
                script {
                    clone("https://github.com/vksr8102/django-notes-app.git", "main")
                }
            }
        }

        stage("Build") {
            steps {
                sh "docker build -t notes-app:latest ."
            }
        }

        stage("Push to Docker Hub") {
            steps {
                script {
                    docker_push(
                        imageName: "vksr2063/notes-app",
                        credentials: "Dockerhubcread"
                    )
                }
            }
        }

        stage("Test") {
            steps {
                echo "Code Test started"
            }
        }

        stage("Deploy") {
            steps {
                echo "Deploy started"
                sh "docker compose down && docker compose up -d"
                echo "Deploy success"
            }
        }
    }
}
