podTemplate(containers: [
    containerTemplate(name: 'shell', image: 'ubuntu', command: 'sleep', args: '99d')
]) {
    node(POD_LABEL) {
        stage('Hello World') {
            container('shell') {
                sh 'echo "Hello, World!"'
            }
        }
    }
}
