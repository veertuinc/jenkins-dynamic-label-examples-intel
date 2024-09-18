def AGENT_LABEL = createDynamicAnkaNode(
  masterVmId: 'c0847bc9-5d2d-4dbc-ba6a-240f7ff08032',
  tag: 'v1',
  nameTemplate: 'nested-cache-builder-example',
  launchMethod: 'ssh',
  credentialsId: 'anka'
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
                masterVmId: 'c0847bc9-5d2d-4dbc-ba6a-240f7ff08032',
                tag: 'v1',
                nameTemplate: 'nested-example-nested',
                saveImage: true,
                suspend: true
                // deleteLatest: true // Dangerous: this removes the latest tag for the Template and that tag may be in-use by other projects in your CI.
              )
            }
          }
        }
        stage("run-on-NESTED_LABEL-vm") {
          agent { label "${NESTED_LABEL}" }
          steps {
            // If buildResults == 'FAILURE', Anka will not push the NESTED_LABEL VM. Example:
            catchError(buildResult: 'FAILURE', stageResult: 'FAILURE') {
              sh 'uname -r'
            }
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
