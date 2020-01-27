  
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

        stage ('Sonar Qube Analysis') {
            steps {
                sh 'mvn sonar:sonar'
            }
        }

       
        stage ('Publish build info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "artifactory"
                )
            }
        }
    }
}
