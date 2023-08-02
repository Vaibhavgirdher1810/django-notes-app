pipeline{
    agent any
    
    stages{
        stage("Code"){
            steps{
                echo "Cloning the code"
                git url: "https://github.com/Vaibhavgirdher1810/django-notes-app.git", branch: "main"
            }
            
        }
        stage("Build"){
            steps{
                echo "Building the images"
                sh "docker build -t notes-app ."
            }
        }
        stage("Push to Dockerhub"){
            steps{
                echo "Pushing your code to  Dockerhub"
                withCredentials([usernamePassword(credentialsId:"dockerhub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag notes-app ${env.dockerHubUser}/notes-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/notes-app:latest"
                    
                }
            }
        }
        stage("Deploy"){
            steps{
                echo "Deploy your container"
                sh "docker-compose down && docker-compose up -d"
            }
        }
        
    }
}
