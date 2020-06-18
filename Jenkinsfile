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
                sh 'mvn clean package sonar:sonar'
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
