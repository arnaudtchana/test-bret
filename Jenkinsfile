pipeline {
  agent any
  
  environment {
    dockerHub = credentials('dockerHub')
    DOCKER_HUB_USERNAME = "206958214313.dkr.ecr.eu-west-2.amazonaws.com"
    APP_NAME = "tello"
    IMAGE_TAG = "${BUILD_NUMBER}"
    IMAGE_NAME = "${DOCKER_HUB_USERNAME}" + "/" + "${APP_NAME}"
  }
  
  stages {
    stage('build') {
      steps {
        echo "On build lapp"
        sh "docker build -t ${IMAGE_NAME.toLowerCase()}:${IMAGE_TAG} ."
      }
      
    }
    stage('pushing to docker hub') {
      steps { 
        echo "On push sur docker hub pour savoir ce qui derange"
        //sh 'echo $dockerHub_PSW | docker login -u $dockerHub_USR --password-stdin'
        sh 'aws ecr get-login-password --region eu-west-2 | docker login --username AWS --password-stdin 206958214313.dkr.ecr.eu-west-2.amazonaws.com'
        sh "docker push ${IMAGE_NAME.toLowerCase()}:${IMAGE_TAG}"
      }
    }
    stage('deploy') {
      steps {
        echo "On deploie lapp en production avec le webhooks sur le projet directement pour voir si le multi branch nouveau test"
      }
    }
  }
}
