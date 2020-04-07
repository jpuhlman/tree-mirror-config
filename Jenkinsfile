pipeline {
    agent any
    options {
        disableConcurrentBuilds()
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
                        [url: 'https://github.com/jpuhlman/tree-mirror']
                        ]
                    ])
            }
        }
    }
}

