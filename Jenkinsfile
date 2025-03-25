pipeline {
    agent {
        docker {
            image 'python3'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh '''
                      python3 --version
                     docker pull  python3
                '''
            }
        }
    }
}

