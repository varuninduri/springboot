  
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
	post {
      always {
        junit '**/reports/junit/*.xml'
      }
   } 	
        }
	stage ('Cobertura coverage report') {
            steps {
               sh 'mvn cobertura:cobertura'
            }
	post {
        always {
          step([$class: 'CoberturaPublisher', coberturaReportFile: '**/coverage/coverage.xml'])
        }
      }	
        }
	stage ('Package to jar ') {
            steps {
               sh 'mvn package'
            }
        } 
    }
}
