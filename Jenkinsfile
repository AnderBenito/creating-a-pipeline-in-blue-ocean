def getEnvFromBranch(branch) {
  if (branch == 'master') {
    return 'production'
  } else {
    return 'staging'
  }
}

pipeline {
  agent {
    docker {
      image 'node:14.15.4-alpine'
      args '-p 3001:3000'
    }

  }
  stages {
    stage('Pre') {
      steps {
        echo 'Pulling from...'+ getEnvFromBranch(env.BRANCH_NAME)
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