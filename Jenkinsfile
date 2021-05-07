pipeline {
  agent {
   label createDynamicAnkaNode(
      masterVmId: '937a445f-9061-4e93-9d5a-3df1ec775132',
      tag: 'v1',
      nameTemplate: 'simple-example-keepalive',
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
