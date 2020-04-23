pipeline {
  agent {
    label createDynamicAnkaNode(
      masterVmId: 'c0847bc9-5d2d-4dbc-ba6a-240f7ff08032',
      tag: 'base:port-forward-22:brew-git:jenkins:openjdk-1.8.0_242'
    )
  }
  stages {
    stage('Begin parallel stage1 execution') {
      parallel {
        stage("parallel builder1 command1") {
          agent {
            label createDynamicAnkaNode(
              masterVmId: 'c0847bc9-5d2d-4dbc-ba6a-240f7ff08032',
              tag: 'base:port-forward-22:brew-git:jenkins:openjdk-1.8.0_242'
            )
          }
          steps {
            echo "builder1 - command1"
          }
        }
        stage("parallel builder1 command2") {
          steps {
            echo "builder1 - command2"
          }
        }
        stage("parallel builder1 command3") {
          steps {
            echo "builder1 - command3"
          }
        }
        stage("parallel builder1 command4") {
          steps {
            echo "builder1 - command3"
          }
        }
        stage("concurrent builder2 command1") {
          agent { 
            label createDynamicAnkaNode(
              masterVmId: 'c0847bc9-5d2d-4dbc-ba6a-240f7ff08032',
              tag: 'base:port-forward-22:brew-git:jenkins:openjdk-1.8.0_242'
            )
          }
          steps {
            echo "builder2 - command1"
          }
        }
      }
    }
  }
}