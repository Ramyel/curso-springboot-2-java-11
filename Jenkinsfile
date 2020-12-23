pipeline {
  agent any
  stages {
    stage('Tools') {
      steps {
        tool 'Maven'
      }
    }

    stage('Getting Code') {
      steps {
        git(url: 'https://github.com/Ramyel/curso-springboot-2-java-11.git', branch: 'master')
      }
    }

    stage('Build / Sonar Analysis') {
      steps {
        withSonarQubeEnv('sonarserver') {
          sh '''mvn clean package sonar:sonar \\
                    -DskipTests \\
                    -Dsonar.projectKey=teste_tres \\
                    -Dsonar.host.url=http://10.200.144.143:9000 \\
                    -Dsonar.login=259cfd4b04c7ed66ad593a303c2c2a7600d1341c'''
        }

      }
    }

    stage('Sonar results') {
      steps {
        waitForQualityGate(credentialsId: 'teste_tres', webhookSecretId: '259cfd4b04c7ed66ad593a303c2c2a7600d1341c', abortPipeline: true)
      }
    }

    stage('Final') {
      steps {
        echo 'Fim do Pipeline'
      }
    }

  }
}