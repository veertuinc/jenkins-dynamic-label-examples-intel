def label = createDynamicAnkaNode(
  masterVmId: 'c0847bc9-5d2d-4dbc-ba6a-240f7ff08032',
  tag: 'v1',
  nameTemplate: 'scripted-example'
)

node(label){
    stage('Sleep') { 
        sh 'sleep 4'
    }
    stage('Do something') { 
        sh 'echo hello'
    } 
}
