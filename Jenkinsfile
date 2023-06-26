pipeline{
    agent any
    tools{
        maven 'MAVEN-3.8.7'
    }
    stages{
        stage('Git CHeckout'){
            steps{
            checkout scmGit(branches: [[name: 'master']], extensions: [], userRemoteConfigs: [[credentialsId: '6477d773-928b-4e02-b3d6-2b110980280c', url: 'https://github.com/PMFayazAhmed/corelogic.git']])
            }
        }
        stage('Build Artifact'){
            steps{
            sh 'mvn package -f pom.xml'
            }
        }
        stage('Tomcat Deploy'){
            steps{
            deploy adapters: [tomcat9(credentialsId: '6b3db44f-1da8-4480-9906-803443b1fa49', path: '', url: 'http://34.134.209.166:8090/')], contextPath: null, war: '**/*.war'
            }    
            }
        stage('Nexus Upload'){
            steps{
            nexusArtifactUploader artifacts: [[artifactId: 'corelogic', classifier: '', file: 'target/Test-PollSCM-Corelogic-Latest.war', type: 'war']], credentialsId: '9bcbd07b-af28-4805-877e-c63ada4fab61', groupId: 'com.adaequare', nexusUrl: '34.170.120.194:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '1.0-SNAPSHOT'
        }
        }
    }
}
