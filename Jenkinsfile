node {
   agent any
   environment {
       //GIT_URL = 'https://github.com/aleksandarz64/docker-web.git'
       APP_NAME = 'docker-web'
       DOCKER_USERNAME = '99118822'
   }
   options {
    disableConcurrentBuilds()
    retry(1)
    skipStagesAfterUnstable()
    timeout(time: 10, unit: 'MINUTES')
    buildDiscarder(logRotator(numToKeepStr: '5', artifactNumToKeepStr: '1'))
}
   stages {
      //stage('Fetch Source code') {
      //   steps {
      //        echo 'Fetch source code'
      //        echo "git url: $GIT_URL"
      //        git url: "$GIT_URL"
      //   }
      //}

      stage ('Build Docker image') {
          steps {
              echo "Building Docker image"
              sh "sudo docker build -t $DOCKER_USERNAME/$APP_NAME:$BUILD_NUMBER ." 
          }
      }

      stage ('Login to Docker HUB') {
          steps {
              echo "Login to Docker Hub"
              withCredentials([string(credentialsId: 'DockerHub_Pwd', variable: 'DockerHub_Pwd')]) {
                   sh "sudo docker login -u $DOCKER_USERNAME -p ${DockerHub_Pwd}"
              }
          }
      }
      stage ('Push Docker image') {
          steps {
              echo "Push Docker image to DockeHub"
              sh "sudo docker image push $DOCKER_USERNAME/$APP_NAME:$BUILD_NUMBER" 
          }
      }
   }
}
