  
pipeline {
    agent any
  tools {
	maven 'maven-3.5.4' 
}
    stages {
        stage ('Clone') {
            steps {
                git branch: 'declarative', url: "https://github.com/varuninduri/springboot.git"
            }
        }

        stage ('Compile') {
            steps {
                sh 'mvn compile'
            }
        }

       
        stage ('sonar qube analysis') {
            steps {
               sh 'mvn sonar:sonar'
            }
        }
	stage ('Unit Testing') {
            steps {
               sh 'mvn test'
            }
 	junit 'target/surefire-reports/*.xml'
        }
	stage ('Cobertura coverage report') {
            steps {
               sh 'mvn cobertura:cobertura'
            }
	cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
        }
	stage ('Package to jar ') {
            steps {
               sh 'mvn package'
            }
        } 
    }
}
