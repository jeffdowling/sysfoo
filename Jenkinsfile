pipeline {
  agent any
  stages {
    stage('build') {
      agent {
        docker {
          image 'git push origin dockerpackage'
        }

      }
      steps {
        echo 'Compiling sysfoo app'
        sh 'mvn compile'
      }
    }

    stage('test') {
      agent {
        docker {
          image 'git push origin dockerpackage'
        }

      }
      steps {
        echo 'Running unit tests'
        sh 'mvn clean test'
      }
    }

    stage('package') {
      agent {
        docker {
          image 'git push origin dockerpackage'
        }

      }
      steps {
        echo 'packaging into a war file'
        sh 'mvn package -DskipTests'
        archiveArtifacts 'target/*.war'
      }
    }

    stage('Docker BnP') {
      agent any
      steps {
        script {
          docker.withRegistry('https://index.docker.io/v1/', 'dockerlogin') {
            def dockerImage = docker.build("jeffdo/sysfoo:v${env.BUILD_ID}", "./")
            dockerImage.push()
            dockerImage.push("latest")
            dockerImage.push("dev")
          }
        }

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