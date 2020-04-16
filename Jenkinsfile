
def LABEL = createDynamicAnkaNode(
  masterVmId: 'c0847bc9-5d2d-4dbc-ba6a-240f7ff08032',
  tag: 'base:port-forward-22:jenkins:openjdk-1.8.0_242'
)

pipeline {
  agent {
       label "${LABEL}"
  }
   stages {
     stage("hello") {
       steps {
         sh "echo hello"
       }
     }
  }
}
