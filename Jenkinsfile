pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        echo 'build stage '
        sh '/opt/maven/apache-maven-3.6.3/bin/mvn clean install -Dlicense.skip=true'
        echo 'end build stage '
      }
    }

    stage('Testing') {
      parallel {
        stage('Test') {
          steps {
            echo 'Test stage'
            echo 'post test'
          }
        }

        stage('tester') {
          steps {
            echo "The tester is ${TESTER}"
            sleep 10
          }
        }

        stage('build num') {
          steps {
            echo "This is build number ${BUILD_ID}"
            sleep 20
          }
        }

      }
    }

  }
  environment {
    TESTER = 'mikasa'
  }
}