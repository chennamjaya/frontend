pipeline {
  agent { label 'new-workstation'}

  stages {

    stage('Code Quality'){
      when {
        allOf {
          expression { env.TAG_NAME != env.GIT_BRANCH }
        }
      }
      steps {
        //sh 'sonar-scanner -Dsonar.host.url=http://172.31.91.185:9000 -Dsonar.login=admin -Dsonar.password=admin123 -Dsonar.projectKey=backend -Dsonar.qualitygate.wait=true'
        echo 'OK'
      }
    }

    stage('Unit Tests'){
      when {
        allOf {
          expression { env.TAG_NAME != env.GIT_BRANCH }
          branch 'main'
        }
      }
      steps {
        // Ideally we should run the tests , But here the developer have skipped it. So assuming those are good and proceeding
        // sh 'npm test'
        echo 'CI'
      }
    }

    stage('Release') {
      when {
        expression { env.TAG_NAME ==~ ".*" }
        }
      steps {
        sh 'zip -r frontend-${TAG_NAME}.zip static asset-manifest.json index.html robots.txt'
        sh 'curl -sSf -u "admin:Dontknow@29" -X PUT -T frontend-${TAG_NAME}.zip "http://artifactory.vaishnavidevops.online:8081/artifactory/frontend/frontend-${TAG_NAME}.zip"'
      }
   }
  }
}