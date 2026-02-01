podTemplate(containers: [
    containerTemplate(name: 'shell', image: 'ubuntu', command: 'sleep', args: '99d')
]) {
    node(POD_LABEL) {
        stage('Hello World') {
            checkout scm
            container('shell') {
                sh 'echo "Hello, World!"'
                sh 'echo new script'
                sh 'echo ${ext}'

                // make a dummy artifact
                sh '''
                  mkdir -p out
                  date > out/dummy.txt
                  echo "ext=${ext}" >> out/dummy.txt
                '''
            }

            // archive it (must run on the agent workspace, outside container is fine)
            archiveArtifacts artifacts: 'out/dummy.txt', fingerprint: true, onlyIfSuccessful: false
        }
    }
}
