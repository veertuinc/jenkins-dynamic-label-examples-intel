pipeline {
  agent {
   label createDynamicAnkaNode(
      masterVmId: 'c0847bc9-5d2d-4dbc-ba6a-240f7ff08032',
      tag: 'v1',
      nameTemplate: 'simple-example',
      keepAliveOnError: true
    )
  }
   stages {
     stage("hello") {
       steps {
         sh "echo hello"
         sh "exit 100"
       }
     }
  }
}
