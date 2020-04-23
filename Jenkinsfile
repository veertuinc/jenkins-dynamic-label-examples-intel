pipeline {
  node(createDynamicAnkaNode(
    masterVmId: 'c0847bc9-5d2d-4dbc-ba6a-240f7ff08032',
    tag: 'base:port-forward-22:brew-git:jenkins:openjdk-1.8.0_242'
  )){
    stage('Begin parallel stage execution') {
      parallel {
        stage("parallel builder agent-1") {
          steps {
            sleep 5
          }
        }
        stage("parallel builder agent-2") {
          steps {
            sleep 5
          }
        }
        stage("parallel builder agent-3") {
          steps {
            sleep 5
          }
        }
        stage("parallel builder agent-4") {
          steps {
            sleep 5
          }
        }
      }
    }
  }

}