node{
    stage("checkout"){
        
    checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'd1dca813-fb7c-4b13-98a4-57c1ecd046ad', url: 'https://github.com/varuninduri/springboot.git']]])
    }
    stage("compile"){
        withMaven(jdk: 'jdk', maven: 'maven-3.5.4') {
 sh label: '', script: 'mvn compile'   
}
    }
      stage("sonar"){
        withMaven(jdk: 'jdk', maven: 'maven-3.5.4') {
 sh label: '', script: 'mvn sonar:sonar'   
}
    }
    stage("junit"){
        withMaven(jdk: 'jdk', maven: 'maven-3.5.4') {
 sh label: '', script: 'mvn test'   
}
junit 'target/surefire-reports/*.xml'
    }
       stage("cobertura"){
        withMaven(jdk: 'jdk', maven: 'maven-3.5.4') {
 sh label: '', script: 'mvn cobertura:cobertura'   
}
cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false
    }
    stage("package"){
        withMaven(jdk: 'jdk', maven: 'maven-3.5.4') {
 sh label: '', script: 'mvn package'   
}
    }
}
