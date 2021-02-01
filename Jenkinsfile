pipeline {
    agent any
    options {
        ansiColor('xterm')
        timestamps()
    }
    triggers {
        pollSCM('')
        issueCommentTrigger('.*test this please.*')
    }
    stages {
        stage('Build') {
            steps {
                sh 'cd kernel && ./gradlew build'
            }
        }
        stage('Publish') {
            when {
                branch 'vinted/master'
            }
            steps {
                sh 'tar -czf sparkex.tar.gz -C beakerx/beakerx/kernel/ sparkex'
                sh 'tar -czf scala.tar.gz -C beakerx/beakerx/kernel/ scala'
                sh 'curl -Sfnv --upload-file sparkex.tar.gz https://nexus.vinted.net/repository/raw-hosted-oom/beakerx/kernels/'
                sh 'curl -Sfnv --upload-file scala.tar.gz https://nexus.vinted.net/repository/raw-hosted-oom/beakerx/kernels/'
            }
        }
    }
}
