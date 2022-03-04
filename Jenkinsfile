node {
    stage ('Checkout'){
        checkout scm
    }

   // stage('Syntax check') {
        // Check PHP syntax
        //sh "/var/lib/jenkins/tools/php_check"
    //}

    stage("SonarQube analysis") {
        steps {
            script {
                def scannerHome = tool 'SonarQube Scanner';
                withSonarQubeEnv('SonarQube Server') {
                    sh 'mvn clean package sonar:sonar'
                }
            }
        }
    }
}
