
def LABEL = createDynamicAnkaNode(
  masterVmId: 'c0847bc9-5d2d-4dbc-ba6a-240f7ff08032',
  tag: 'base:port-forward-22:brew-git:openjdk-1.8.0_242:jenkins'
)

pipeline {
  agent {
    label "${LABEL}"
  }
  stages {
    stage("hello") {
      steps {
        sh "echo testing123 > testfile"
        sh "echo testing1234 > testfile2"
        sh "echo testing12345 > testfile3"
      }
    }
    stage("archive") {
      archiveArtifacts artifacts: 'testfile', fingerprint: true
    }
    stage("archive2") {
      archiveArtifacts artifacts: 'testfile2', fingerprint: true
      archiveArtifacts artifacts: 'testfile3', fingerprint: true
    }
  }
}
