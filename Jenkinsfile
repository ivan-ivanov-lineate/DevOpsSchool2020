pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        sh 'echo "build"'
      }
    }

    stage('test') {
      parallel {
        stage('test') {
          steps {
            sh 'echo "test"'
          }
        }

        stage('test2') {
          steps {
            sh 'echo "test2"'
          }
        }

      }
    }

    stage('deploy') {
      steps {
        sh 'echo "deploy"'
      }
    }

  }
}
