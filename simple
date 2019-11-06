
def LABEL = createDynamicAnkaNode(masterVmId: 'e1173284-39df-458c-b161-a54123409280')

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
