pipeline {
    agent any
    stages {
        stage('Run in Docker') {
            steps {
                script {
                    docker.image('python').inside {
                        sh 'python --version'
                    }
                }
            }
        }
    }
}
