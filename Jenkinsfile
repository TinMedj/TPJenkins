pipeline {
  agent any
  stages {
    stage('build') {
      post{
        failure{
          mail(subject: 'Jenkins', body: 'Build Succefull', from: 'ft_medjkoune@esi.dz', to: 'ft_medjkoune@esi.dz')
        }
      }
      steps {
        sh 'gradle build'
        sh 'gradle jar'
        sh 'gradle javadoc'
        archiveArtifacts 'build/libs/*.jar'
        archiveArtifacts 'build/docs/javadoc/'
      }
    }
    stage('Mail Notification') {
      steps {
        mail(subject: 'Jenkins', body: 'Build Succefull', from: 'ft_medjkoune@esi.dz', to: 'ft_medjkoune@esi.dz')
      }
    }
    stage('Code Analysis') {
      parallel {
        stage('Code Analysis') {
          steps {
            withSonarQubeEnv('sonarqube') {
              bat 'E:\\2CSil\\OUTILS\\sonar-scanner-cli-3.2.0.1227-windows\\sonar-scanner-3.2.0.1227-windows\\bin\\sonar-scanner '
            }

            waitForQualityGate true
          }
        }
        stage('Test reporting') {
          steps {
            jacoco()
          }
        }
      }
    }
    stage('Deployment') {
      when{
            NOT{
              changeRequest target : 'master'
            }
          }
      steps {
        sh 'gradle uploadArchives'
      }
    }
    stage('Slack Notification') {
      steps {
        slackSend(attachments: 'Deloyment suceffull', message: 'success in deployment ')
      }
    }
  }
}
