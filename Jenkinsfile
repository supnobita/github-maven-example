pipeline {
  agent any
  stages {
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            echo 'Building Maven code code'
            sh 'apt-get install build-essential libcurl4-openssl-dev libxml2-dev libssl-dev libfuse-dev libjson-c-dev pkg-config -y'
            sh './configure'
            sh 'make'
          }
        }
        stage('newstate') {
          steps {
            echo 'abc_test_add_newstate'
          }
        }
      }
    }
    stage('Test') {
      steps {
        echo 'Testing..'
      }
    }
    stage('Deploy') {
      when {
        expression {
          currentBuild.result == null || currentBuild.result == 'SUCCESS'
        }

      }
      steps {
        echo 'Deploying....'
        sh 'make install'
      }
    }
  }
}