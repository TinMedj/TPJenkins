pipeline {
  agent any
  stages {
    stage('build') {
      steps {
        mail(subject: 'jenkins', body: 'success', from: 'ft_medjkoune@esi.dz', to: 'ft_medjkoune@esi.dz')
      }
    }
    stage('sonarqube') {
      steps {
        withSonarQubeEnv('sonarqube') {
          sh 'E:\\2CSil\\TP OUTILS\\Sonarqube\\sonar-scanner-cli-3.2.0.1227-windows\\sonar-scanner-3.2.0.1227-windows\\bin\\sonar-scanner'
        }

        waitForQualityGate true
      }
    }
  }
}