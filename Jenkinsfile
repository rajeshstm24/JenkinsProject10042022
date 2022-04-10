pipeline {
  agent any
  stages {
    stage('Dev-Build') {
      steps {
        git(url: 'https://github.com/rajeshstm24/WebApp.git', branch: 'master')
        script {
          try{
            bat 'start /min stopApp.bat'
          }catch(Exception e){
            echo 'Nothing running on 9002 port'
          }
        }

        bat 'mvn install'
        bat 'set JENKINS_NODE_COOKIE=dontKillMe && start /min startApp.bat'
      }
    }

  }
}