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
        stage('Descargar Git') {
            steps {
                   git credentialsId: '726eb245-32d1-4417-ab4a-0033fdd16e5e', url: 'https://github.com/Aldavid13/practica1.git'  
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
                        case 'master':
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
}
}

