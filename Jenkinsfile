 pipeline {
     agent { label "dev-server" }
     stages{
         stage("Clone Code"){
             steps{
                 git url: "https://github.com/sprasadpujari/Node-app-todo-cicd", branch: "main"
             }
         }
         stage("Build and Test"){
             steps{
                 sh "docker build . -t sprasadpujari/node-app-test-new:latest"
             }
         }
         stage("Push to Docker Hub"){
             steps{
               withCredentials([usernamePassword(credentialsId :'dockerHub',passwordVariable:'dockerHubPassword',usernameVariable: 'dockerHubUser')]) {
            	sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
                sh "docker push sprasadpujari/node-app-test-new:latest"
                
                 }
             }
         }
         stage("Deploy"){
             steps{
                 sh "docker-compose down && docker-compose up -d"
             }
         }
     }
 }
