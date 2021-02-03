pipeline {
  agent {
    node {
      label 'node-slave-1'
    }

  }
  stages {
    stage('Pre') {
      steps {
        echo 'Pulling from...'+getEnvFromBranch(env.BRANCH_NAME)
      }
    }

    stage('Build') {
      steps {
        sh 'npm install'
      }
    }

    stage('Test') {
      steps {
        sh './jenkins/scripts/test.sh'
      }
    }

    stage('Deliver') {
      steps {
        sh './jenkins/scripts/deliver.sh'
        sh './jenkins/scripts/kill.sh'
      }
    }

  }
  environment {
    CI = 'true'
    NODE_ENV = getEnvFromBranch(env.BRANCH_NAME)
  }
}