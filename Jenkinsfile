def foo = sh(returnStdout: true, script: "git tag --sort version:refname | tail -1").trim()
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
                   sh 'echo $TAG_NAME'
                   sh 'echo $BUILD_TAG'
                   sh '''sed -i "s|tag|$BUILD_NUMBER|g" deployment-services-practica-01-jenkins.yaml
			sed -i "s|namespace-var|$BRANCH_NAME|g" deployment-services-practica-01-jenkins.yaml
			cat deployment-services-practica-01-jenkins.yaml
			'''
		   script {
    			// crear variable para el TAG
			TAG = sh(returnStdout: true, script: 'git tag')				
							}
		   sh 'echo $TAG'					
                   }
        }
        stage('Variable para el TAG') {
            steps {
              script {
    			// crear variable para el TAG
			gitTag=sh(returnStdout: true, script: "git tag")	
		}
		 sh 'echo $foo'
		 
            
             
        }
}
}
}

