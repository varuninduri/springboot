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
                branch: "master",
                url: "https://gs_mrt@bitbucket.org/gs_mrt/simple-java-maven-app.git"
            )
            }
        }
    }
