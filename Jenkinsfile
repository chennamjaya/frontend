pipeline {
  agent { label 'new-workstation'}

  stages {

    stage('Code Quality') {
      when {
        expression { env.TAG_NAME !=~ ".*" }
            }
      steps {
        sh 'sonar-scanner -Dsonar.host.url=http://172.31.34.168:9000 -Dsonar.login=admin -Dsonar.password=admin1234 -Dsonar.projectKey=frontend -Dsonar-qualitygate.wait=true'
      }
    }

    stage('Release') {
      when {
        expression { env.TAG_NAME ==~ ".*" }
            }
      steps {
        sh 'env'
        echo 'CI'
      }
   }
 }
 
} 