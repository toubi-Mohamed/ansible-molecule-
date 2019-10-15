pipeline {

  agent any

  stages {

    stage ('Get latest code') {
      steps {
        git 'https://github.com/toubi-Mohamed/ansible-molecule-.git'
      }
    }

    stage ('Setup Python virtual environment') {
      steps {
        sh '''
          pip3 install virtualenv
          virtualenv virtenv
          source /var/lib/jenkins/workspace/CI-ansible/virtenv/bin/activate
          pip install --upgrade ansible molecule docker
        '''
      }
    }

    stage ('Display versions') {
      steps {
        sh '''
          /var/lib/jenkins/workspace/CI-ansible/virtenv/bin/activate
          docker -v
          python -V
          ansible --version
          molecule --version
        '''
      }
    }

    stage ('Molecule test') {
      steps {
        sh '''
          source virtenv/bin/activate
          molecule converge
        '''
      }
    }

  }

}

