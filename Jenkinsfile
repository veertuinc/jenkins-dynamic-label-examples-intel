pipeline {
  agent none
  stages {
    stage('Begin parallel stage execution') {
      parallel {
        stage("parallel builder agent-1") {
          agent {
              label "ssh"
          }
          steps {
              sleep 5
          }
        }
        stage("parallel builder agent-2") {
          agent {
              label "ssh"
          }
          steps {
              sleep 5
          }
        }
        stage("parallel builder agent-3") {
          agent {
              label "ssh"
          }
          steps {
              sleep 5
          }
        }
        stage("parallel builder agent-4") {
          agent {
              label "ssh"
          }
          steps {
              sleep 5
          }
        }
      }
    }
  }
}