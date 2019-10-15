pipeline {

  agent any

  stages {

    stage ('Get latest code') {
      steps {
        git 'https://github.com/toubi-Mohamed/ansible-molecule-.git'
      }
    }

    stage ('Install Dependcies') {
      steps {
        sh '''
          pip3 install virtualenv
          virtualenv virtenv
          source CI-ansible/virtenv/bin/activate
          pip3 install molecule
          pip3 install ansible 
          pip3 install docker 
        '''
      }
    }

    stage ('Display versions') {
      steps {
        sh '''
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

