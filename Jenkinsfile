def gv

pipeline {
  
  agent any
  parameters {
    //string(name: 'VERSION', defaultValue: '', description: 'version to deploy on prod')
    choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
    booleanParam(name: 'executeTests', defaultValue: true, description: '')
  }
  environment {
    NEW_VERSION = '1.3.0'
    //SERVER_CREDENTIALS = credentials('MyGitHub')
  }

  stages {
    stage("init") {
      steps {
        script {
          gv = load "script.groovy"
        }
      }
    }

    stage("build") {
      steps {
        //echo 'building the application...'
        //echo "building version ${NEW_VERSION}"
        script {
          gv.buildApp()
        }
      }
    }

    stage("test") {
      when {
        expression {
          params.executeTests
        }
      }
      steps {
        //echo 'testing the application...'
        script {
          gv.testApp()
        }
      }
    }
    stage("deploy") {
      steps {
        //echo 'deploying the application...'
        //echo "deploying version ${params.VERSION}"
        script {
          gv.deployApp()
        }
        //withCredentials([
          //usernamePassword(credentials: 'MyGitHub', usernameVariable: USER, passwordVariable: PWD)
        //]) {
          //sh "some script ${USER} ${PWD}"
      }
    }
  }
}
