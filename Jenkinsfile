pipeline {
    agent {
        docker {
            image 'python:3.10' // tu peux spécifier une version stable ici
        }
    }
    stages {
        stage('Build') {
            steps {
                sh '''
                    python --version
                '''
            }
        }
    }
}
