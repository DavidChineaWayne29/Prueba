pipeline {
  agent any

  parameters {
    choice(name: 'ENV', choices: ['prod', 'dev', 'test', 'local'], description: 'Select the env')
  }

  enviroment {
    ENV = ${params.ENV}
  }

  stages {
    stage('Install Dependencies') {
      steps {
        script {
          if (isUnix()) {
            sh 'npm install'
          } else {
            bat 'npm install'
          }
        }
      }
    }
    stage('Run Playwright Tests') {
      steps {
        script {
          if (isUnix()) {
            sh "\$env:ENV=${ENV}; npx playwright test"
          } else {
            bat "set ENV=${ENV} && npx playwright test"
          }
        }
      }
    }
  }
}
