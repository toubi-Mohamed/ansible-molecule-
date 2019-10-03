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
          export HTTP_PROXY=http://192.168.100.59::8080
          export HTTPS_PROXY=http://192.168.100.59::8080
          pip3 install virtualenv
          virtualenv virtenv
          source virtenv/bin/activate
          pip install --upgrade ansible molecule docker
        '''
      }
    }

    stage ('Display versions') {
      steps {
        sh '''
          source virtenv/bin/activate
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
          molecule test
        '''
      }
    }

  }

}

