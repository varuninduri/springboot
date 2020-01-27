  
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
    }
}
