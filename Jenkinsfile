pipeline {
  agent any
  stages {
    stage('Dev-Build') {
      steps {
        git(url: 'https://github.com/rajeshstm24/WebApp.git', branch: 'master', poll: true)
        script {
          try{
            bat "StopApp.bat"
          }catch(Exception e){
            echo "nothing running on 9002"
          }
        }

        bat 'mvn install'
        bat 'set JENKINS_NODE_COOKIE=dontKillMe && start /min startApp.bat'
      }
    }

    stage('QA-Test') {
      parallel {
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