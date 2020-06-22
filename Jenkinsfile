#!/usr/bin/env groovy
      pipeline {
        agent any
            tools {
            maven "Maven"
            }
           
        stages {
        	stage('Getting code from SCM') {
            steps {
            git 'https://github.com/Ramyel/curso-springboot-2-java-11.git'
              echo 'Building..'
            	}
        	}
          	stage("build & SonarQube analysis") {
            steps {
              withSonarQubeEnv('sonarserver') {
                  sh "mvn sonar:sonar \
  -Dsonar.projectKey=teste_quatro \
  -Dsonar.host.url=http://10.200.144.143:9000 \
  -Dsonar.login=5081a54fd38ed432540c9ce9b263ce7855f7ec63"
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
