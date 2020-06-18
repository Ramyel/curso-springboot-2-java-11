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
}