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
                python3 --version
                docker pull  python
                '''
            }
        }
    }
}
}}}}

