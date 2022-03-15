node {
    stage ('Checkout'){
        checkout scm
    }

   // stage('Syntax check') {
        // Check PHP syntax
        //sh "/var/lib/jenkins/tools/php_check"
    //}

  stage('SonarQube analysis') {
        // requires SonarQube Scanner 2.8+
        def scannerHome = tool 'SonarQubePlugins';
        withSonarQubeEnv('SonarQubeServer') {

          def projectKey=env.JOB_NAME.replaceAll('%2F','.')
          projectKey=projectKey.replaceAll('/','.')

          echo "projectKey: ${projectKey}"

          sh "${scannerHome}/bin/sonar-scanner -D sonar.projectKey=${projectKey}  -D sonar.sources=. -D sonar.host.url='http://35.154.197.67:9000/' -D sonar.exclusions=bootstrap/**,config/**,database/**,docker/**,public/**,storage/**,tests/**,vendor/**"
          stash includes: ".sonar/report-task.txt", name: 'sonar'
        }
  }

}
