pipeline {

    agent any

    stages{

        stage('build') {
            steps {
                sh 'mvn package'
            }
        }

        // PUBLIC REPOSITORY
        stage('image - create') {
            steps {
                sh "echo creating image..."
                script {
                    def build = docker.build("public.ecr.aws/k6s1i7x9/auth-service:0.0.1-SNAPSHOT", ".")
                }
            }
        }
        stage('image - push') {
            steps {
                sh "echo pushing image to ecr..."
                script {
                    docker.withDockerRegistry('https://public.ecr.aws/k6s1i7x9/auth-service', 'ecr:us-east-1:ecr-credentials') {
                        docker.image("public.ecr.aws/k6s1i7x9/auth-service:0.0.1-SNAPSHOT").push()
                        // sh 'docker push public.ecr.aws/k6s1i7x9/gateway-service:0.0.1-SNAPSHOT'
                    }
                }
            }
        }
        // PRIVATE REPOSITORY - WORKING FINE
        // stage('image - create and push') {
        //     steps {
        //         sh "echo pushing image to ecr..."
        //         script {
        //             def build = docker.build("153294646920.dkr.ecr.us-east-1.amazonaws.com/asde-batch5:0.0.1-SNAPSHOT", ".")
        //             withDockerRegistry(
        //                 credentialsId: 'ecr:us-east-1:ecr-credentials', 
        //                 url: 'https://153294646920.dkr.ecr.us-east-1.amazonaws.com/asde-batch5') {
        //                 docker.image("153294646920.dkr.ecr.us-east-1.amazonaws.com/asde-batch5:0.0.1-SNAPSHOT").push()
        //             }
        //         }
        //     }

    }
    post {
        always {
            echo 'cleaning workspace...'
            cleanWs()
        }
    }
}