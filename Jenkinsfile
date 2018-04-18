pipeline {
  agent any
  stages {
    stage('compile') {
      steps {
        echo 'Step 1. Hello World'
      }
    }
    stage('package') {
      steps {
        echo 'Step 2. Second time Hello'
	echo 'Step 3. Third time Hello'  

      }
    }
    stage('deploy') {
      steps {
       echo 'Step 4. last time Hello' 
      }
    }
  }
}
