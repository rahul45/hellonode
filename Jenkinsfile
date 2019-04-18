
String dockerHost = 'hub.docker.com'
String namespace = 'rbhadour'
String tagBase = "$dockerHost/$namespace"

String webRepo = 'hellonode'
pipeline {
    agent any
    environment {
        DOCKER_CREDENTIALS_ID = 'docker-hub-cred'
        DEVOPS_METRICS_ENABLED = 'false'
    }
    stages {
        stage('Web: Build and Deploy Docker Image to DTR') {
            agent {
                label 'docker-nodejs-slave'
            }
            steps {
                glDockerImageBuildPush tag: "$tagBase/$webRepo",
                        repository: "$webRepo",
                        namespace: "$namespace",
                        dockerCredentialsId: "$env.DOCKER_CREDENTIALS_ID"
            }
        }
    }
    post {
        always {
            echo 'Email Notification'
            emailext body: "Successfully done" +
                    "Yes baby!!",
                    subject: "Docker Image Creation",
                    to: 'rahulsinghb99@gmail.com'
        }
    }

}
