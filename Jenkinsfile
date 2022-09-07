pipeline {
    agent any
    environment {
        registry = "<dockerhub-username>/<repo-name>"
        registryCredential = '<dockerhub-credential-name>'
    }
    tools {
        gradle "GRADLE7"
        jdk "openjdk17"
    }

    stages {
        stage('Build Gradle') {
            steps {
                sh 'gradle build'
                   }
        }
        
        stage('Change Variable tag y namespaces') {
            steps {
                sh '''sed -i "s|tag|$BUILD_NUMBER|g" deployment-services-practica-01-jenkins.yaml
			sed -i "s|namespace-var|$BRANCH_NAME|g" deployment-services-practica-01-jenkins.yaml
			cat deployment-services-practica-01-jenkins.yaml
			'''
                   }
        }
        
       stage('Building image') {
           steps {
            step([$class: 'DockerBuilderPublisher', cleanImages: true, cleanupWithJenkinsJobDelete: false, cloud: 'docker', dockerFileDirectory: '.', fromRegistry: [credentialsId: 'dockerhub', url: 'https://hub.docker.com/repository/docker/aldavid/practica-demo-$BRANCH_NAME'], pushCredentialsId: 'dockerhub', pushOnSuccess: true, tagsString: '''aldavid/practica-demo-$BRANCH_NAME:$BUILD_NUMBER
                aldavid/practica-demo-$BRANCH_NAME:latest'''])

           }
        
        }
       
        
        stage('Deploy practica-02-jenkins App') {
            steps {
                withCredentials(bindings: [
                      string(credentialsId: 'minikube-jenkins', variable: 'api_token')
                      ]) {
                        sh 'kubectl --token $api_token --server https://192.168.49.2:8443 --insecure-skip-tls-verify=true config view '
                        }

            }
      }
        
    }
}

