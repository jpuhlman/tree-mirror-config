pipeline {
    agent any
    options {
        disableConcurrentBuilds()
    }
    stages {
        stage('Initialize') {
            steps {
            git 'https://github.com/jpuhlman/tree-mirror'
            }
        }
    }
}

