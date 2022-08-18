pipeline {
  agent any
  
  environment {
    dockerHub = credentials('dockerHub')
    DOCKER_HUB_USERNAME = "arnaudrhopen"
    APP_NAME = "bret-app-test"
    IMAGE_TAG = "${BUILD_NUMBER}"
    IMAGE_NAME = "${DOCKER_HUB_USERNAME}" + "/" + "${APP_NAME}"
  }
  
  stages {
    stage('build') {
      steps {
        echo "On build lapp"
        sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
      }
      
    }
    stage('pushing to docker hub') {
      steps {
        echo "On push sur docker hub pour savoir ce qui derange"
        sh 'echo $dockerHub_PSW | docker login -u $dockerHub_USR --password-stdin'
        sh "docker push ${IMAGE_NAME}:${IMAGE_TAG}"
      }
    }
    stage('deploy') {
      steps {
        echo "On deploie lapp en production avec le webhooks sur le projet freestyle"
      }
    }
  }
}
