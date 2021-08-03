pipeline {

    agent any

    stages{

        stage('build') {
            steps {
                sh 'mvn package'
            }
        }

        stage('image - create and push') {
            steps {
                sh "echo creating image and pushing to ecr..."
                script {
                    def build = docker.build("153294646920.dkr.ecr.us-east-1.amazonaws.com/asde-batch5:0.0.1-SNAPSHOT", ".")
                    withDockerRegistry(
                        credentialsId: 'ecr:us-east-1:ecr-credentials', 
                        url: '153294646920.dkr.ecr.us-east-1.amazonaws.com/asde-batch5') {
                        docker.image("153294646920.dkr.ecr.us-east-1.amazonaws.com/asde-batch5:0.0.1-SNAPSHOT").push()
                    }
                }
            }
        }
    }
    post {
        always {
            echo 'cleaning workspace...'
            cleanWs()
        }
    }
}