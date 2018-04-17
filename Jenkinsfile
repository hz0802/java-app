pipeline {
  agent any
  stages {
    stage('compile') {
      steps {
        sh 'mvn clean compile'
      }
    }
    stage('package') {
      steps {
        sh 'mvn package -DskipTests'
      }
    }
    stage('deploy') {
      steps {
        sh 'nohup java -jar target/my-first-app-1.0-SNAPSHOT-fat.jar &'
      }
    }
  }
}
