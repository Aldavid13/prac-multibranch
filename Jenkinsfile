pipeline {
    agent any
    environment {
        registry = "<dockerhub-username>/<repo-name>"
        registryCredential = '<dockerhub-credential-name>'
        GLOBAL_ENVIRONMENT = 'NO_DEPLOYMENT'
    }
    tools {
        gradle "GRADLE7"
        jdk "openjdk17"
    }

    stages {
        stage('Descargar Git') {
            steps {
                   git credentialsId: '726eb245-32d1-4417-ab4a-0033fdd16e5e', url: 'https://github.com/Aldavid13/prac-multibranch.git'  
                   }
        }
        stage('Setup environment') {
            steps {
                echo 'Setup environment'
                
                script {
                    // Determine whether this is a test or a staging / production build                    
                    switch (env.BRANCH_NAME) {
                        case 'develop':
                            GLOBAL_ENVIRONMENT = 'test'
                            break
                        case 'Staging':
                            GLOBAL_ENVIRONMENT = 'staging'
                            break
                        default: 
                            GLOBAL_ENVIRONMENT = 'NO_DEPLOYMENT'
                            break
                    }

                    // Get tag on current branch
                    TAG = sh(returnStdout: true, script: 'git tag --points-at HEAD')

                    if (TAG && GLOBAL_ENVIRONMENT == 'staging') {
                        echo 'Build for production'
                        
                        
        
       
            }
      }
        
    		}
	}


	stage('verificar variable de entorno') {
            steps {
                   sh 'echo $BRANCH_NAME'
                   sh 'echo ahora con la global environment'
                   sh 'echo $GLOBAL_ENVIRONMENT'
                   sh '''sed -i "s|tag|$BUILD_NUMBER|g" deployment-services-practica-01-jenkins.yaml
			cat deployment-services-practica-01-jenkins.yaml
			sed -i "s|namespace-var|$BRANCH_NAME|g" deployment-services-practica-01-jenkins.yaml
			cat deployment-services-practica-01-jenkins.yaml
		   '''
                   }
        }
}
}

