#!/usr/bin/env groovy
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
            steps {
              withSonarQubeEnv('sonarserver') {
               def mvnHome = tool 'maven-3.6.3'
                    sh "'${mvnHome}/bin/mvn' -f backend/pom.xml clean package sonar:sonar"
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
