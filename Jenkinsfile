pipeline {

    agent any

    statges{

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
                    docker.withRegistry("153294646920.dkr.ecr.us-east-1.amazonaws.com/asde-batch5", "ecr-credentials") {
                        docker.image("153294646920.dkr.ecr.us-east-1.amazonaws.com/asde-batch5:0.0.1-SNAPSHOT").push()
                    }
                }
            }
        }
    }
}