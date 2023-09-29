pipeline{
    agent any
    
    stages{
        stage("Code"){
            steps{
                echo "Clonnig the code from github"
                git url: "https://github.com/D-singh121/jenkins-declarative-CICD-django-app.git", branch: "main"
            }
            
        }
        
        stage("Build"){
             steps{
                echo "Building the image through docker"
                sh "docker build --no-cache -t my-notes-app ."
            }
        }
        
        stage("Push to Docker hub"){
            steps{
                echo " Pushing the image to the  Docker Hub"
                withCredentials ([usernamePassword(credentialsId:"dockerHub_id",passwordVariable: "dockerHubPass", usernameVariable:"dockerHubUser")]){
                sh "docker tag my-notes-app ${env.dockerHubUser}/my-note-app:latest "
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-note-app:latest "
                }
                
            }
        }
        
        stage("Deploy"){
             steps{
                echo "Deploying the container"
               // sh "docker run -d -p 8000:8000 devesh121/my-note-app:latest"
                sh "docker-compose down && docker-compose up -d"
            }
        }
    }
}
