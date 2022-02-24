pipeline {
    agent any
    options {
        disableConcurrentBuilds()
    }
    triggers {
         cron('H H/12 * * *')
    }
    environment {
        EMAIL_TO = 'jpuhlman@mvista.com'
    }
    stages {
        stage('Initialize') {
            steps {
                    checkout([
                        $class: 'GitSCM',
                        branches: [[name: "master"]],
                        doGenerateSubmoduleConfigurations: false,
                        extensions: [
                            [$class: 'RelativeTargetDirectory', relativeTargetDir: "tools"],
                        ],
                        submoduleCfg: [],
                        userRemoteConfigs: [
                        [url: 'https://github.com/oomforge/tree-mirror.git']
                        ]
                    ])
            }
        }
        stage('Run update') {
            steps {
                sh 'tools/bin/update.sh'
            }
        }
    }
    post {
        failure {
            emailext body: 'Check console output at $BUILD_URL to view the results. \n\n ${CHANGES} \n\n -------------------------------------------------- \n${BUILD_LOG, maxLines=100, escapeHtml=false}', 
            to: EMAIL_TO, 
            subject: 'Build failed in Jenkins: $PROJECT_NAME - #$BUILD_NUMBER'
        }
    }
}

