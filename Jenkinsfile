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
    stage('Push to Registry') {
      steps {
        sh 'docker login $Docker_Reg -u $icp_user -p $icp_pass'
        sh 'docker push $Docker_Reg/$Img_Space/$App_Name:latest'
      }
    }
    stage('ICP_Login-1') {
      steps {
        sh '''
        export BLUEMIX_HOME=/root/.bluemix
        bx pr login -a $icp_server -u $icp_user -p $icp_pass -c $icp_acctid --skip-ssl-validation
        bx pr cluster-config $icp_clustername
        kubectl get nodes
        helm init --client-only
        '''
      }
    }
    stage('ICP_Deploy') {
      steps {
        sh 'kubectl run java-app --image=$Docker_Reg/$Img_Space/$App_Name:latest'
        sh 'kubectl expose deployment/java-app --port=80 --target-port=80'

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
