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
            sh '''cd /opt/dockerdep ;
cp /var/lib/jenkins/workspace/fasto_master/POC_PI_AWS-ear/target/POC_PI_AWS-ear.ear /opt/dockerdep/POC_PI_AWS-ear.ear;
ansible-playbook --user master fastplay.yml;
'''
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