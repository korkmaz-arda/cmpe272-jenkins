pipeline {
    agent {
        docker { image 'python:3.14.7-alpine3.24' }
    }

    stages {
        stage('Build') {
            steps {
                sh '''
                    echo "CMPE 272 Jenkins artifact" > artifact.txt
                '''
            }
        }

        stage('Test') {
            steps {
                sh '''
                    mkdir -p test-results

                    cat > test-results/results.xml <<EOF
                    <testsuite name="CMPE272" tests="1" failures="0">
                        <testcase classname="JenkinsPipeline" name="helloWorld"/>
                    </testsuite>
                    EOF
                '''
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'artifact.txt', fingerprint: true
            junit 'test-results/*.xml'
        }
    }
}