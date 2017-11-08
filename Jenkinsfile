node {
    def nodeHome = tool name: 'node-7.8.0', type: 'jenkins.plugins.nodejs.tools.NodeJSInstallation'
    env.PATH = "${nodeHome}/bin:${env.PATH}"

    stage('check tools') {
        sh "node -v"
        sh "npm -v"
    }

    stage('checkout') {
        checkout scm
    }

    stage('npm install') {
        sh "npm install"
    }

    //stage('unit tests') {
    //    sh "ng test"
    //}

    //stage('protractor tests') {
    //  sh "npm run e2e"
    //}
    stage('SonarQube') {
        def scannerHome = tool 'SQScanner';
        withSonarQubeEnv {
            sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=angular:pipeline:my-app-pipeline -Dsonar.projectName=AngularPipeline -Dsonar.projectVersion=1.0 -Dsonar.sources=src"
        }
    }
}
