pipeline {
  agent any
  stages {
    stage('Git checkout'){
      steps{
        git 'https://github.com/nduka145/tomcat8.git'
      }
    }
  stage ('Build Virtualenv') {
    steps {
        sh """
          set +x
          echo "Building Virtualenv"
          python3 -m venv env
          . env/bin/activate
          pip install --upgrade pip
          pip install -U -r requirements.txt
        """
      }
    }
    
  stage ('Molecule Test') {
    steps {
        sh """
           set +x
           echo "Running Molecule Test"
           . env/bin/activate
           molecule test
        """
        }
      }    
  }
}
