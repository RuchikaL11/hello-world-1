pipeline {
    agent any
  tools {
      maven 'M2_HOME'
  }
  stages{
    stage('build'){
      steps{
          sh script: 'mvn clean install package'
      }
    }
    stage('upload'){
      steps{
          script{
            def mavenPom = readMavenPom file: 'pom.xml'
            nexusArtifactUploader artifacts: [
                [
                    artifactId: 'maven-project', 
                    classifier: '', 
                    file: 'webapp/target/webapp.war', 
                    type: 'war'
                ]
            ], 
            credentialsId: 'admin', 
            groupId: 'com.example.maven-project', 
            nexusUrl: '54.161.184.91:8081', 
            nexusVersion: 'nexus3', 
            protocol: 'http', 
            repository: 'maven-snapshots', 
            version: "${mavenPom.version}"
          }
      }
    }
  }

}
