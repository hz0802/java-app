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
          docker build -t $Docker_Reg/$Img_Space/$App_Name:latest
	  '''
      }
    }
    stage('Push to Registry') {
      steps {
        sh 'docker login $Docker_Reg -u $icp_user -p $icp_pass'
        sh 'docker push $Docker_Reg/$Img_Space/$App_Name:latest'
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
  environment {
    icp_server = 'https://9.220.79.110:8443'
    icp_user = 'admin' 
    icp_pass = 'MySecretP4ssw0RD'
    icp_acctid = 'id-mycluster-account'
    icp_clustername = 'mycluster'
    Docker_Reg = 'https://icp-console-d6eec5d435c34072.elb.us-west-2.amazonaws.com:8500'
    Img_Space = 'default'
    App_Name = 'java-app'
    rel_name = 'mydemo'
  }
}
