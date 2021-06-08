pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'Compiling sysfoo app'
        sh 'mvn compile'
      }
    }

    stage('test') {
      steps {
        echo 'Running unit tests'
        sh 'mvn clean test'
      }
    }

    stage('package') {
      steps {
        echo 'packaging into a war file'
        sh 'mvn package -DskipTests'
        archiveArtifacts 'target/*.war'
      }
    }

  }
  tools {
    maven 'Maven 3.6.3'
  }
  post {
    always {
      echo 'This pipeline is completed..'
    }

  }
}