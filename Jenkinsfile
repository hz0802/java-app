pipeline {
  agent any
  stages {
    stage('compile') {
      steps {
        echo 'Step 1. Hello World'
      }
    }
    stage('Building_Image') {
      steps {
	sh '''
	  cd ${WORKSPACE}
	  REPO="ecr-k8s-app"
	  docker build --no-cache -t ${REPO}:${BUILD_NUMBER} .
	  '''
      }
    }
    stage('deploy') {
      steps {
       echo 'Step 4. last time Hello' 
      }
    }
  }
}
