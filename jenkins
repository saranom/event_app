/* groovylint-disable CompileStatic, DuplicateStringLiteral, NestedBlockDepth */
pipeline {
    environment {
        registry = 'asia.gcr.io/map-ceremony-0306/node_helloworld'
        registryCredential = 'gcr:map-ceremony-0306'
        dockerImage = ''
    }
    agent any

    stages {
        stage('Building our image') {
            steps {
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }
        stage('Deploy our image') {
            steps {
                script {
                    docker.withRegistry('https://asia.gcr.io/map-ceremony-0306', 'gcr:map-ceremony-0306') {
                        dockerImage.push()
                    }
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}

