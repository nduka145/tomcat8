pipeline {
  agent any
  stages {
    stage('Git checkout'){
      steps{
        git branch: 'molecule', url: 'https://github.com/nduka145/tomcat8.git'
      }
    }
  stage ('Build Virtualenv') {
    steps {
        sh """
          set +x
          echo "Building Virtualenv"
          python3 -m venv env
          . env/bin/activate
          pip3 install --upgrade pip
          python3 -m pip ansible testinfra molecule podman python-vagrant ansible-lint flake8 molecule[lint,ansible,podman] jmespath
        """
      }
    }
    
  stage ('Molecule Test') {
    steps {
        sh """
           set +x
           echo "Running Molecule Test"
           . env/bin/activate
           cd roles/tomcat
           molecule test
        """
        }
      }    
  }
}
