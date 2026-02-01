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
                  mkdir -p out1
                  date > out1/dummy.txt
                  echo "ext=${ext}" >> out1/dummy.txt
                  date > out1/dummy2.txt
                  echo "ext=${ext}" >> out1/dummy2.txt
                '''
                            sh '''
                  mkdir -p out2
                  date > out2/dummy.txt
                  echo "ext=${ext}" >> out2/dummy.txt
                '''
            }

            // archive it (must run on the agent workspace, outside container is fine)
            archiveArtifacts artifacts: 'out1/**,out2/dummy.txt', fingerprint: true, onlyIfSuccessful: false
        }
    }
}
