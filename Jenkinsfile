pipeline {
  agent any
  stages {
    stage('compile') {
      steps {
        sh 'sh \'mvn clean compile\''
      }
    }
    stage('Package') {
      steps {
        sh 'sh \'mvn package -DskipTests\''
      }
    }
    stage('Deploy') {
      steps {
        sh 'sh \'nohup java -jar target/my-first-app-1.0-SNAPSHOT-fat.jar &\''
      }
    }
  }
}