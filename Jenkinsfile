#!/bin/sh
pipeline {
    agent {
        docker {
            image 'python:3.9'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'docker version'
                sh 'docker pull python:3.9'
            }
        }
    }
}
