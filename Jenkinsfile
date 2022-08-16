pipeline {
  agent any
  
  environment {
    dockerHub = credentials('dockerHub')
  }
  
  stages {
    stage('build') {
      steps {
        echo "On build lapp"
        sh 'docker build -t test-bret-with-jenkins:1.0 .'
      }
      
    }
    stage('pushing to docker hub') {
      steps {
        echo "On teste lapp"
        sh 'docker tag test-bret-with-jenkins:1.0 arnaudrhopen/test-bret-jks:1.0'
        sh 'echo $dockerHub_PSW | docker login -u $dockerHub_USR --password-stdin'
        sh 'docker push arnaudrhopen/test-bret-jks:1.0'
      }
    }
    stage('deploy') {
      steps {
        echo "On deploie lapp"
      }
    }
  }
}
