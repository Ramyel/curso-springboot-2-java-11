pipeline {
  agent any
  stages {
    stage('Getting code from Github') {
      steps {
        git(url: 'https://github.com/Ramyel/curso-springboot-2-java-11.git', branch: 'master')
      }
    }

    stage('Build & Sonar Analysis') {
      steps {
        withSonarQubeEnv(installationName: 'sonarserver', credentialsId: '5081a54fd38ed432540c9ce9b263ce7855f7ec63') {
          sh '''"mvn clean package sonar:sonar \\
                    -DskipTests \\
                    -Dsonar.projectKey=teste_tres \\
                    -Dsonar.host.url=http://10.200.144.143:9000 \\
                    -Dsonar.login=259cfd4b04c7ed66ad593a303c2c2a7600d1341c"
'''
        }

      }
    }

    stage('Quality Gate') {
      steps {
        waitForQualityGate(credentialsId: 'teste_quatro', webhookSecretId: '5081a54fd38ed432540c9ce9b263ce7855f7ec63', abortPipeline: true)
      }
    }

  }
}