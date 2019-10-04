pipeline {
    agent any
    tools {
        maven "Maven"   
    }    
    stages {
        stage('Compile-Build-Test') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('SonarQube Analysis'){
            steps{
                withSonarQubeEnv('sonarqube'){
                    sh 'mvn sonar:sonar'
                }
            }
        }
        stage('Nexus Repository'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'Calc', classifier: '', file: 'pom.xml', type: 'jar']], credentialsId: 'nexus-credentialss', groupId: 'com.aea', nexusUrl: '18.224.155.110:8081/nexus/', nexusVersion: 'nexus2', protocol: 'http', method: 'post', repository: 'devopstraining', version: '0.0.1-SNAPSHOT'
            }
        }
    }
}
