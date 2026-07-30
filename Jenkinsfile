@Library("Shared") _
pipeline {
    agent { label 'vinod' }

    stages {
        stage("Hello from library"){
            steps{
            script{
                hello()
                }
             }
        }
        stage("Code") {
            steps {
                script{
                    clone("https://github.com/tejalthakare95/django-notes-app1.git", "main")
                }
                
                echo "Code cloning successful."
            }
        }

        stage("Build") {
            steps {
                script{
                    docker_build("notes-app", "latest", "tejalthakare95")
                }
            }
        }

        stage("Push to DockerHub") {
            steps {
               script{
                   docker_push("notes-app", "latest", "tejalthakare95")
               }
            }
        }

        stage("Deploy") {
            steps {
                echo "Deploying the application..."

                sh '''
                    docker compose down && true
                    docker compose up -d --build
                '''
            }
        }
    }
}
