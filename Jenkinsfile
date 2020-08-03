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
            sh '/opt/maven/apache-maven-3.6.3/bin/mvn sonar:sonar -Dsonar.host.url=http://192.168.157.128:8081 -Dlicense.skip=true'
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