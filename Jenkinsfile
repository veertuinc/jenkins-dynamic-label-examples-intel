

def AGENT_LABEL = createDynamicAnkaNode(
  masterVmId: 'e56b4aaf-0797-42dd-9ebe-41908bf10a4d', 
  launchMethod: 'ssh', 
  credentialsId: 'anka-default-user'
)
def NESTED_LABEL = ''

pipeline {
  agent {
    label "${AGENT_LABEL}"
  }
  options {
    skipStagesAfterUnstable()
  }
  stages {
    stage("command-in-$AGENT_LABEL") {
      steps {
        sh "uname -a"
      }
    }
    stage("nested-vm-stages") {
      stages {
        stage("launch-nested-vm") {
          steps {
            script {
            NESTED_LABEL = createDynamicAnkaNode(
              launchMethod: 'jnlp', 
              masterVmId: 'e56b4aaf-0797-42dd-9ebe-41908bf10a4d', 
              saveImage: true, 
              suspend: true,
              deleteLatest: true
            )
            }
          }
        }
        stage("run-on-nested-vm") {
          agent { label "${NESTED_LABEL}" }
          try {
            sh 'uname -r; exit 5'
          } catch (Exception e) {
            currentBuild.result = 'FAILURE'  //  fail the build on any error
          }
        }
        stage("generate-tag-from-nested-vm") {
          steps {
            ankaGetSaveImageResult shouldFail:true, timeoutMinutes: 120
          }
        }
      }
    }
  }
}
