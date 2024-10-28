pipeline {
  agent any
  stages {

     stage('Maven Build') {
        steps { 
          sh "mvn clean package && cp target/*.jar . "
     }
    }
     
     stage('Docker Image Build') {     
        steps {
              sh 'sudo docker build -t myjava-image . '
               }
             }
        stage('Docker image push') {
           steps {
                 // withCredentials([usernamePassword(credentialsId: '82377f3d-eaad-4d26-8e68-bdb06c13e4d8', passwordVariable: 'Password', usernameVariable: 'Username')]) {
                 // sh "sudo docker login -u ${env.Username} -p ${env.Password}"
                 sh "sudo docker login -u shruti1725 -p nisharajeev"
                 sh "sudo docker image tag myjava-image shruti1725/myjava-image:test"
                 sh "sudo docker image tag myjava-image shruti1725/myjava-image:${BUILD_NUMBER}"
                 sh "sudo docker image push shruti1725/myjava-image:${BUILD_NUMBER}" 
               } 
             }  
          }
      stage('Deploy app') {
         steps {
           sh 'ls -ltr'
           //sh 'kubectl apply -f app-deploy.yaml'
            sh 'sudo docker container run -d --name testcont shruti1725/myjava-image:test'
        }
     }
    }

//  post {
//    always {
//      deleteDir() /* cleanup the workspace */
//    }
//  }
 }
