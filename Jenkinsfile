pipeline {
    agent {
        label 'jenkins-agent-3'
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                bat 'if exist out rmdir /s /q out'
                bat 'mkdir out'
                bat 'javac --release 8 -d out src\\hello\\Hello.java'
            }
        }

        stage('Run') {
            steps {
                bat 'java -cp out hello.Hello'
                bat 'echo Build_OK > artifact.txt'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'artifact.txt,out/**', allowEmptyArchive: false
        }
    }
}
