pipeline {
    agent any
      stage("build & SonarQube analysis") {
          node {
              withSonarQubeEnv('sonarserver') {
                 sh 'mvn clean package sonar:sonar'
              }    
          }
      }
      
      stage("Quality Gate"){
          timeout(time: 1, unit: 'HOURS') {
              def qg = waitForQualityGate()
              if (qg.status != 'OK') {
                  error "Pipeline aborted due to quality gate failure: ${qg.status}"
              }
          }
      } 
}
