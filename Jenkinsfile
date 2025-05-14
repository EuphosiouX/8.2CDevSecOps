pipeline { 
  agent any 
 
  stages { 
    stage('Checkout') { 
      steps { 
        git branch: 'main', url: ' https://github.com/EuphosiouX/8.2CDevSecOps.git' 
      } 
    } 
 
    stage('Install Dependencies') { 
      steps { 
        sh 'npm install' 
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
 
  } 
} 
