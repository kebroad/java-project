pipeline { 
  agent none 
  
  stages {
    stage('Unit Tests'){
      agent{
        label 'CentOs'
      }
      steps {
        sh 'ant -f test.xml -v'
        junit 'reports/result.xml'
      }
    }
    stage ('build') {
      agent{
        label 'CentOs'
      }
      steps{
        sh 'ant -f build.xml -v'
        echo 'updated!'
      }
    
      post {
        success{
          archiveArtifacts artifacts: 'dist/*.jar', fingerprint: true
        }
      }
    }
    stage ('deploy') {
      agent{
        label 'CentOs'
      }
      steps {
        sh "cp dist/rectangle_${env.BUILD_NUMBER}.jar /var/www/html/rectangles/all/"
      }
    }
    stage("Running on CentOS") { 
      agent {
        label 'CentOs'
      }
      steps {
        sh "wget http://kebroad1.mylabserver.com/rectangles/all/rectangle_${env.BUILD_NUMBER}.jar"
        sh "java -jar rectangle_${env.BUILD_NUMBER}.jar 3 4"
      }
    }
    stage("Test on Debian") {
      agent {
        docker 'openjdk:8u171-jre-alpine'
      }
      steps {
        sh "wget http://kebroad2.mylabserver.com/rectangles/all/rectangle_${env.BUILD_NUMBER}.jar"
        sh "java -jar rectangle_${env.BUILD_NUMBER}.jar 3 4"
      }
    }
  }
}
