pipeline{
  agent any
  stages{
    stage("Clone Code"){
      steps{
        echo "Cloneing the code"
        git url:"https://github.com/Nilesh-0203/Jenkins-declarative-node-todo-app.git", branch:"master"
      }
    }
    stage("Build Code"){
      steps{
        echo "BUilding the code"
        sh "docker build -t note-app ."
      }
    }
    stage("Push to dockerHub"){
      steps{
        echo "pushing to docker hub"
        withCredentials([usernamePassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
            sh "docker tag note-app ${env.dockerHubUser}/note-app:latest"
            sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
            sh "docker push ${env.dockerHubUser}/note-app:latest"
        }
      }
    }
    stage("Deploy"){
      steps{
        echo "Deploying"
        //sh "docker run -d -p 8000:8000 nilesh0203/note-app:latest"
        sh "docker-compose down && docker-compose up -d"
      }
    }
  }
}
