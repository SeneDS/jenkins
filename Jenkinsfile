pipeline {
    agent {
        docker {
            image 'python'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh '''
                     python --version
                     docker pull python
                '''
            }
        }
    }
}

