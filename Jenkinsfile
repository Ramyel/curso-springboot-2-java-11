      pipeline {
        agent any
        stages {
        	stage('Getting code from SCM') {
            steps {
            git 'https://github.com/Ramyel/curso-springboot-2-java-11.git'
              echo 'Building..'
            	}
        	}
          	stage("build & SonarQube analysis") {
            agent any
            steps {
              withSonarQubeEnv('sonarserver') {
                mvn sonar:sonar \
  -Dsonar.projectKey=teste_dois \
  -Dsonar.host.url=http://10.200.144.143:9000 \
  -Dsonar.login=0998ec18481ad4b2eac28bf46ba386b6aef0a8e1
              }
            }
          }
          stage("Quality Gate") {
            steps {
              timeout(time: 1, unit: 'HOURS') {
                waitForQualityGate abortPipeline: true
              }
            }
          }
        }
      }
