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
    stage('Pushing_Image_To_ECR') {
      steps {
       sh '''
	REG_ADDRESS="436112110102.dkr.ecr.us-east-2.amazonaws.com/ecr-k8s-app"
	REPO="ecr-k8s-app"
	docker tag ${REPO}:${BUILD_NUMBER} ${REG_ADDRESS}/${REPO}:${BUILD_NUMBER}
	docker push ${REG_ADDRESS}/${REPO}:${BUILD_NUMBER}
    '''
      }
    }
  }
}
