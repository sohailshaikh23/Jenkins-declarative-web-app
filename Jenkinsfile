pipeline {
    agent any 
    
    stages{
        stage("Clone the  Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/sohailshaikh23/Jenkins-declarative-web-app.git", branch: "master"
                
            }
        }
        stage("Build the raw code"){
            steps {
                echo "Building the image"
                sh "docker build -t my-note-app ."
               
                
                
            }
        }
        stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                 withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")])
                {
                sh "docker tag my-note-app ${env.dockerHubUser}/note-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/note-app:latest"
                }
                
                
            }
        }
        stage("Deploy the app"){
            steps {
                echo "Deploying the container"
                sh "docker-compose down && docker-compose up -d"
                
            }
        }
    }
}
