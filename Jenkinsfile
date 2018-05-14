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
        sh '''
        docker login $Docker_Reg -u $icp_user -p $icp_pass
        docker push $Docker_Reg/$Img_Space/$App_Name:latest
        '''
      }
    }
    stage('Deploy onto ICP ') {
      steps {
        sh '''
        export PATH=$PATH:/usr/local/bin
        export BLUEMIX_HOME=/var/lib/jenkins/.bluemix
        bx pr login -a $icp_server -u $icp_user -p $icp_pass -c $icp_acctid --skip-ssl-validation
		bx pr cluster-config $icp_clustername
        kubectl get nodes
        kubectl run java-app-deployment --image=$Docker_Reg/$Img_Space/$App_Name:latest
        helm init --client-only
        '''
      }
    }
    stage('Approval to proceed') {
      parallel {
        stage('sending email') {
          steps {
            mail (to: 'haimo.zhang@ibm.com',
				  subject: "Job '${env.JOB_NAME}' is waiting for input",
				  body: "Please go to '${JOB_LINK}'"
				  )
          }
        }
        stage('approval') {
          steps {

            input 'ok to proceed ?'
          }
        }
      }
    }
    stage('sucess !') {
      steps {
        echo 'Great, Java app build and deployed in icp successfully !'
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
	JOB_LINK = 'http://52.11.131.45:8083/blue/organizations/jenkins/java-app/detail/master'
  }
}