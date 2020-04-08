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
  stages {
    stage("command-in-AGENT_LABEL-vm") {
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
                deleteLatest: true // Dangerous: only use if the Template isn't holding other project tags.
              )
            }
          }
        }
        stage("run-on-NESTED_LABEL-vm") {
          agent { label "${NESTED_LABEL}" }
          steps {
            // If buildResults == 'FAILURE', Anka will not push the NESTED_LABEL VM. Example:
            // catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
            //   sh 'uname -r; exit 5'
            // }
            sh 'uname -r'
          }
        }
        stage("check-generated-tag-from-nested-vm") {
          steps {
            ankaGetSaveImageResult shouldFail:true, timeoutMinutes: 120
          }
        }
      }
    }
  }
}
