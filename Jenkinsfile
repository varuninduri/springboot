  
pipeline {
    agent any
    stages {
        stage ('Clone') {
            steps {
                git branch: 'declarative', url: "https://github.com/varuninduri/springboot.git"
            }
        }

        stage ('Artifactory configuration') {
            steps {
                rtServer (
                    id: "jfrog_artifactory",
                    url: "http://localhost:8081/artifactory",
                    credentialsId: artifactory
                )

                rtMavenDeployer (
                    id: "maven-3.5.4.1",
                    serverId: "jfrog_artifactory",
                    releaseRepo: "libs-release-local",
                    snapshotRepo: "libs-snapshot-local"
                )

                rtMavenResolver (
                    id: "maven-3.5.4.2",
                    serverId: "jfrog_artifactory",
                    releaseRepo: "libs-release",
                    snapshotRepo: "libs-snapshot"
                )
            }
        }

        stage ('Exec Maven') {
            steps {
                rtMavenRun (
                    tool: 'maven-3.5.4', // Tool name from Jenkins configuration
                    pom: 'pom.xml',
                    goals: 'clean install',
                    deployerId: "maven-3.5.4.1",
                    resolverId: "maven-3.5.4.2"
                )
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
