// adapted from https://www.cloudbees.com/sites/default/files/declarative-pipeline-refcard.pdf
pipeline {
  agent any
  environment {
    SOME_PATH='/usr/local/bin/'
  }
  options {
    timeout time:6, unit: 'HOURS'
  }
  stages {
    stage('Test') {
      steps {
        sh 'echo Executing tests... | tee tests.log'
      }
    }
    stage('Archive') {
      when {
        expression { !fileExists("experiment.txt") }
      }
      steps {
        archive 'tests.log'
      }
    }
  }
  post {
    always {
      deleteDir()
    }
    failure {
      mail to: "maintainer@example.com", subject: "Build failure", body: "${env.BUILD_URL}"
    }
  }
}
