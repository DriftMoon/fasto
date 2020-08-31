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

    stage('Docker Image creation') {
      parallel {
        stage('Image Creation') {
          steps {
            echo 'Test stage'
            sh '''cp POC_PI_AWS-ear/target/POC_PI_AWS-ear.ear /opt/dockerdep/POC_PI_AWS-ear.ear ;
cd /opt/dockerdep ;
ansible-playbook --user jenkins /opt/dockerdep/fastplay.yml ;
'''
            echo 'post test'
          }
        }

        stage('build num') {
          steps {
            echo "This is build number ${BUILD_ID}"
            sleep 20
          }
        }

        stage('Env') {
          steps {
            sh 'whoami'
            echo 'im here!!'
            sh '''pwd;
ls -l;'''
          }
        }

      }
    }

    stage('Deployment creation') {
      steps {
        echo 'Preparing the deployment ---> '
        sh 'sudo su - ansible -c " sudo ansible-playbook --user root /home/master/k8s/Ansiblek8sdeployment.yml"'
      }
    }

    stage('Service Creation') {
      steps {
        echo 'Service Creation ---->'
        sh 'sudo su - ansible -c " sudo ansible-playbook --user root /home/master/k8s/Ansiblek8sservice.yml"'
      }
    }

  }
  environment {
    TESTER = 'mikasa'
  }
}