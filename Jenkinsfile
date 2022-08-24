
// def LABEL = createDynamicAnkaNode(
//   masterVmId: 'c0847bc9-5d2d-4dbc-ba6a-240f7ff08032',
//   tag: 'v1',
//   launchMethod: 'ssh',
//   credentialsId: 'anka'
// )

pipeline {
  agent {
    label createDynamicAnkaNode(
      masterVmId: 'c0847bc9-5d2d-4dbc-ba6a-240f7ff08032',
      tag: 'v1',
      launchMethod: 'ssh',
      credentialsId: 'anka'
    )
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
      steps {
        archiveArtifacts artifacts: 'testfile', fingerprint: true
      }
    }
    stage("archive2") {
      steps {
        archiveArtifacts artifacts: 'testfile2', fingerprint: true
        archiveArtifacts artifacts: 'testfile3', fingerprint: true
      }
    }
  }
}
