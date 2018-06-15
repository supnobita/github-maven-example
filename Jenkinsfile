pipeline {
  agent any
  stages {
    
      stage('SonarQube analysis') {
         steps {
    withSonarQubeEnv('sonarqube209') {
      // requires SonarQube Scanner for Maven 3.2+
      sh '/var/jenkins_home/maven/bin/mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
    }
  }
  }
    stage('Build') {
      parallel {
        stage('Build') {
          steps {
            echo 'Building Maven code code'
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
