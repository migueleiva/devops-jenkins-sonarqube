//START-OF-SCRIPT
node {
    def SONARQUBE_HOSTNAME = 'sonarqube'

    def GRADLE_HOME = "/opt/gradle/gradle-5.0"
    sh "${GRADLE_HOME}/bin/gradle tasks"

    stage('prep') {
        git url: 'https://github.com/cloudacademy/devops-webapp.git'                
    }

    stage('build') {
        sh "${GRADLE_HOME}/bin/gradle build"
    }

    stage('sonar-scanner') {
      def sonarqubeScannerHome = tool name: 'sonar', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
      withCredentials([string(credentialsId: 'sonar', variable: 'sonarLogin')]) {
        sh "${sonarqubeScannerHome}/bin/sonar-scanner -e -Dsonar.host.url=http://sonarcloud.io -Dsonar.token=1a719712a6f2c0e4673a1b286cadee149e34e7bd -Dsonar.projectName=WebApp -Dsonar.projectVersion=${env.BUILD_NUMBER} -Dsonar.projectKey=GS -Dsonar.sources=src/main/ -Dsonar.tests=src/test/ -Dsonar.java.binaries=build/**/* -Dsonar.language=java"
      }
    }

}
//END-OF-SCRIPT
