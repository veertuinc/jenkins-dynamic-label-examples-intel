

def AGENT_LABEL = createDynamicAnkaNode(masterVmId: 'e56b4aaf-0797-42dd-9ebe-41908bf10a4d', launchMethod: 'ssh', credentialsId: 'anka-default-user')
def NESTED_LABEL = ''

pipeline {
  agent {
       label "${AGENT_LABEL}"
  }
   stages {
     stage("test") {
       steps {
         sh "uname -a"
       }
     }
     stage("nested") {
       stages {
         stage("new agent") {
           steps {
             script {
              NESTED_LABEL = createDynamicAnkaNode(launchMethod: 'jnlp', masterVmId: 'e56b4aaf-0797-42dd-9ebe-41908bf10a4d', 
                                                  saveImage: true, suspend: true, deleteLatest: true)
             }
           }
         }
         stage("run on nested") {
           agent { label "${NESTED_LABEL}" }
           steps {
             sh 'uname -r'
             sh 'sleep 20'
           }
         }
         stage("wait for finish") {
           steps {
             ankaGetSaveImageResult shouldFail:true, timeoutMinutes: 120
           }
         }
       }
     }
  }
}
