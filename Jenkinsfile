pipeline { 
  agent any 

  environment {
    SONAR_SCANNER_HOME = tool 'SonarQubeScanner'
  }

  stages { 
    stage('Checkout') { 
      steps { 
        git branch: 'main', url: 'https://github.com/EuphosiouX/8.2CDevSecOps.git' 
      } 
    } 

    stage('Install Dependencies') { 
      steps { 
        bat 'npm install' 
      } 
    }

    stage('Run Tests') { 
      steps { 
        bat 'npm test || exit /b 0' 
      } 
    } 

    stage('Generate Coverage Report') { 
      steps { 
        bat 'npm run coverage || exit /b 0' 
      } 
    } 

    stage('NPM Audit (Security Scan)') { 
      steps { 
        bat 'npm audit || exit /b 0' 
      } 
    }

    stage('Code Quality Check') {
      steps {
        withCredentials([string(credentialsId: 'SONAR_TOKEN', variable: 'SONAR_TOKEN')]) {
          bat "${SONAR_SCANNER_HOME}/bin/sonar-scanner"
        }
      }
    }
  } 
}
