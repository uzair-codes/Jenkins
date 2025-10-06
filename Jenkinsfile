pipeline {
  agent any

  stages {
    stage('Checkout') {
      steps {
        // if job is Pipeline from SCM, Jenkins will checkout automatically.
        echo 'Checking out code...'
        checkout scm
      }
    }

    stage('Setup Python') {
      steps {
        sh 'python3 --version || true'
        sh 'python3 -m venv venv || true'
        sh '. venv/bin/activate && pip install --upgrade pip || true'
        sh '. venv/bin/activate && pip install pytest || true'
      }
    }

    stage('Run Tests') {
      steps {
        sh '. venv/bin/activate && pytest -q'
      }
    }
  }

  post {
    success {
      echo "Tests passed ✅"
    }
    failure {
      echo "Build failed ❌"
    }
  }
}

