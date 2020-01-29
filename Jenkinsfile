@Library('Jenkins_Shared_Library@master') _
 
pipeline {
    agent any
    
    
    tools { 
        maven 'maven-3.5.4' 
        jdk 'jdk' 
    }
    
    stages {
        stage('Git Checkout') {
            steps {
            gitCheckout(
                branch: "shared_lib",
                url: "https://github.com/varuninduri/springboot.git",
                credentials: "d1dca813-fb7c-4b13-98a4-57c1ecd046ad"
            )
            }
        }
    stage ('Clean') {
            steps {
                mavenTasks( step: "clean" )                
            }
        }
    stage ('Compile') {
            steps {
                mavenTasks( step: "compile" )                
            }
        }
    stage ('sonar analysis') {
            steps {
                mavenTasks( step: "sonar" )                
            }
        }
    stage ('test') {
            steps {
                mavenTasks( step: "test" )
             junit 'target/surefire-reports/*.xml'
            }
        }
    stage ('coverage') {
            steps {
                mavenTasks( step: "coverage" )
             cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
            }
        }
    stage ('package') {
            steps {
                mavenTasks( step: "package" )                
            }
        }  
    }
}
