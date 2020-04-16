def AGENT_LABEL = createDynamicAnkaNode(
  masterVmId: 'c0847bc9-5d2d-4dbc-ba6a-240f7ff08032',
  tag: 'base:port-forward-22:brew-git:jenkins:openjdk-1.8.0_242',
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
        sh "uname -a" // Run within the first AGENT_LABEL VM instance
      }
    }
    stage("nested-vm-stages") {
      stages {
        stage("launch-nested-vm") { // Creates a second VM instance which will, after job completion, push to the Registry.
          steps {
            script {
              NESTED_LABEL = createDynamicAnkaNode(
                launchMethod: 'jnlp', 
                masterVmId: 'c0847bc9-5d2d-4dbc-ba6a-240f7ff08032',
                tag: 'base:port-forward-22:brew-git:jenkins:openjdk-1.8.0_242',
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
            sh 'uname -r' // Run within the NESTED_LABEL VM instance
          }
        }
        stage("check-generated-tag-from-nested-vm") {
          steps {
            script {
              def getPushResult = ankaGetSaveImageResult( shouldFail: true, timeoutMinutes: 120 )
              echo "ankaGetSaveImageResult Returned: $getPushResult"
            }
          }
        }
      }
    }
  }
}
