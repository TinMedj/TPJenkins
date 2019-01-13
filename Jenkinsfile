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
          sh 'sonar-scanner'
        }

        waitForQualityGate true
      }
    }
  }
}