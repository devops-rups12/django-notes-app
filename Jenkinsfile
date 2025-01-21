pipeline{

agent {label "jenkins"}

stages{ 
    stage("code"){
        steps{
            echo "this is cloneing the code"
            git url: "https://github.com/LondheShubham153/django-notes-app.git",branch:"main"
            echo "code cloning succussful"
        }
    }
    stage("build"){
        steps{
            echo "this is building the code"
            sh "docker build -t node-app:latest ."
        }
    }
    stage("push to dockerhub"){
        steps{
            withCredentials([usernamePassword(
                'credentialsId':"dockerhubcre",
                passwordVariable:"dockerHubPass",
                usernameVariable:"dockerHubUser")]){
            echo "this is pusing the image to docker hub"
            sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
            sh "docker image tag node-app:latest ${env.dockerHubUser}/node-app:latest"
            sh "docker push ${env.dockerHubUser}/node-app:latest"
            }
        }
    }
    stage("deploy"){
        steps{
            echo "this is deploying the code"
            sh "docker compose up -d "
        }
    }
    
}

}
