pipeline {
  agent any
  stages {
    stage('Dev-Build') {
      steps {
        git(url: 'https://github.com/rajeshstm24/WebApp.git', branch: 'master', poll: true)
        bat 'StopApp.bat'
        bat 'mvn install'
        bat 'StartApp.bat'
      }
    }

    stage('QA-Test') {
      parallel {
        stage('QA-Test') {
          steps {
            echo 'parallel '
          }
        }

        stage('UI Automation') {
          steps {
            git(url: 'https://github.com/rajeshstm24/WebAppUiAutomation.git', branch: 'master', poll: true)
            bat 'mvn test'
          }
        }

        stage('API Automation') {
          steps {
            git(url: 'https://github.com/rajeshstm24/WebAppApiAutomation.git', branch: 'master')
            bat 'mvn test'
          }
        }

        stage('Performance Test') {
          steps {
            echo 'JMeter tests'
          }
        }

      }
    }

    stage('UAT') {
      steps {
        echo 'UAT testing'
      }
    }

  }
}