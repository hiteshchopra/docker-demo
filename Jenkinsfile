pipeline {
    environment {
        imageName = 'hiteshchopra/docker-jenkins'
        registryCredential = 'dockerhub'
        dockerImage = ''
    }
    agent any

    stages {
        stage('Cloning git') {
            steps {
                git([url: 'https://github.com/hiteshchopra/docker-demo.git', branch: 'master'])
            }
        }
        stage('Building image') {
            steps {
                script {
                    dockerImage = docker.build imageName
                }
            }
        }
        stage('Deploy image') {
            steps {
                script {
                    docker.withRegistry('', registryCredential) {
                        dockerImage.push('$BUILD_NUMBER')
                        dockerImage.push('latest')
                    }
                }
            }
        }
    }
}
