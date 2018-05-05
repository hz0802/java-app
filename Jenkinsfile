pipeline {
  agent any
  stages {
    stage('compile') {
      steps {
        echo 'Step 1. Hello World'
	sh 'whoami'
      }
    }
    stage('Building_Image') {
      steps {
        sh '''
          cd ${WORKSPACE}
          docker build -t $Docker_Reg/$Img_Space/$App_Name:latest .
          '''
      }
    }
  }
  environment {
    icp_server = 'https://ec2-18-219-192-91.us-east-2.compute.amazonaws.com:8443'
    icp_user = 'hzhang'
    icp_pass = '1ibmpass'
    icp_acctid = 'id-mycluster-account'
    icp_clustername = 'mycluster'
    Docker_Reg = 'mycluster.icp:8500'
    Img_Space = 'default'
    App_Name = 'java-app'
    rel_name = 'mydemo'
  }
}
