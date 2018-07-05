pipeline { 
  agent any
  stages {
    stage ('build') {
      steps{
        sh 'ant -f build.xml -v'
        echo 'updated!'
      }
    }
  }
  post {
    always{
      archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true
      
    }
    
  }
}
