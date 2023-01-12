pipeline{
    agent any
    tools{
        maven 'MAVEN_3.8.7'
    }
    stages{
        stage('Git Checkout'){
            steps{
                checkout scmGit(branches: [[name: 'master']], extensions: [], userRemoteConfigs: [[credentialsId: '12ba6a55-b4b9-4447-aaa8-003314537a78', url: 'https://github.com/PMFayazAhmed/corelogic.git']])
            }
        }
        stage('Build Stage'){
            steps{
                sh 'mvn package -f pom.xml'
            }
        }
        stage('Tomcat Deploy'){
            steps{
                deploy adapters: [tomcat9(credentialsId: 'f307bf5f-88f5-41c0-b120-1d9a8c4ec267', path: '', url: 'http://34.125.242.217:8090/')], contextPath: null, war: '**/*.war'
            }
        }
        stage('Nexus Upload'){
            steps{
                nexusArtifactUploader artifacts: [[artifactId: 'corelogic', classifier: '', file: 'target/PollSCM-Corelogic.war', type: 'war']], credentialsId: 'd3e45a3f-2a5b-4407-bdaa-f49a324e86c3', groupId: 'com.adaequare', nexusUrl: '34.125.204.227:8081/', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '1.0-SNAPSHOT'
            }
        }
    }
}
