pipeline {
  agent any
  stages {
    stage('Compile') {
      steps {
        sh 'mvn clean compile'
      }
    }
    stage('Package') {
      steps {
        sh 'mvn package -DskipTests'
      }
    }
    stage('Deploy') {
      steps {
        sh 'nohup java -jar target/my-first-app-1.0-SNAPSHOT-fat.jar &'
      }
    }
  }
}