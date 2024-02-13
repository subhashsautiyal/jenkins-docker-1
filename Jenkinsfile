pipeline {
    agent any 
    
    stages{
        stage("Clone Code"){
            steps {
                echo "Cloning the code"
                git url:"https://github.com/subhashsautiyal/jenkins-docker-1.git", branch: "main"
            }
        }
        stage("Build"){
            steps {
                echo "Building the image"
                sh "docker build -t my-react-app ."
            }
        }
        stage("Push to Docker Hub"){
            steps {
                echo "Pushing the image to docker hub"
                withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
                sh "docker tag my-react-app ${env.dockerHubUser}/my-react-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-react-app:latest"
                }
            }
        }
        stage("Deploy"){
            steps {
                echo "Deploying the container"
               # sh "docker-compose down && docker-compose up -d"
                sh "docker-compose up -d --no-deps --force-recreate"
                
            }
        }
    }
}
