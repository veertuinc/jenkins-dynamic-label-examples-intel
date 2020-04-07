
def LABEL = createDynamicAnkaNode(masterVmId: 'e56b4aaf-0797-42dd-9ebe-41908bf10a4d')

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
