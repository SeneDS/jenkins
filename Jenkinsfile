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
                     docker version 
                     docker pull python
                '''
            }
        }
    }
}
