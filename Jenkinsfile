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
cp /var/lib/jenkins/workspace/fasto_master/POC_PI_AWS-ear/target/POC_PI_AWS-ear.ear /opt/dockerdep/POC_PI_AWS-ear.ear ;
ansible-playbook --user jenkins /opt/dockerdep/fastplay.yml ;
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

        stage('meme') {
          steps {
            sh 'whoami'
          }
        }

      }
    }

    stage('Deployment creation') {
      steps {
        echo 'Preparing the deployment ---> '
        sh 'sudo su - ansible -c "sh sudo ansible-playbook --user root /home/master/k8s/Ansiblek8sdeployment.yml"'
      }
    }

    stage('Service Creation') {
      steps {
        echo 'Service Creation ---->'
        sh 'sudo su - ansible -c "sh sudo ansible-playbook --user root /home/master/k8s/Ansiblek8sservice.yml"'
      }
    }

  }
  environment {
    TESTER = 'mikasa'
  }
}