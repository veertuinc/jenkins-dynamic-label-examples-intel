pipeline {
  agent none
  stages {
    stage('Begin parallel stage1 execution') {
      parallel {
        stage("parallel builder1 command1") {
          agent {
            label createDynamicAnkaNode(
              masterVmId: 'c0847bc9-5d2d-4dbc-ba6a-240f7ff08032',
              tag: 'base:port-forward-22:brew-git:openjdk-1.8.0_242:jenkins',
              nameTemplate: 'simple-parallel-example-builder1'
            )
          }
          steps {
            echo "builder1 - command1"
            sh "hostname"
          }
        }
        stage("parallel jenkins host command1") {
          steps {
            echo "builder1 - command2"
            sh "hostname"
          }
        }
        stage("concurrent builder2 command1") {
          agent { 
            label createDynamicAnkaNode(
              masterVmId: 'c0847bc9-5d2d-4dbc-ba6a-240f7ff08032',
              tag: 'base:port-forward-22:brew-git:openjdk-1.8.0_242:jenkins',
              launchMethod: 'ssh',
              nameTemplate: 'simple-parallel-example-builder2'
            )
          }
          steps {
            echo "builder2 - command1"
            sh "hostname"
          }
        }
      }
    }
  }
}
