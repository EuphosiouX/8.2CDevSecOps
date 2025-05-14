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
        sh 'npm test || exit /b 0' // Allows pipeline to continue despite test failures 
      } 
    } 

    stage('Generate Coverage Report') { 
      steps { 
        // Ensure coverage report exists 
        sh 'npm run coverage || exit /b 0' 
      } 
    } 

    stage('NPM Audit (Security Scan)') { 
      steps { 
        sh 'npm audit || exit /b 0' // This will show known CVEs in the output 
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
