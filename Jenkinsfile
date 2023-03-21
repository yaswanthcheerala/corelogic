pipeline{
    agent any
    tools{
        maven 'Maven 3.9.0'
    }
    stages{
        stage('Git checkout'){
            steps{
                checkout scmGit(branches: [[name: 'master']], extensions: [], userRemoteConfigs: [[credentialsId: '4e38f06a-8511-4aa7-b550-70679c3ca0c0', url: 'https://github.com/PMFayazAhmed/corelogic.git']])
            }
        }
        stage('code Build'){
            steps{
            sh 'mvn package -f pom.xml'
            }
        }

        stage('Tomcat deployment'){
            steps{
            deploy adapters: [tomcat9(credentialsId: 'dad5aa26-1956-4f72-8835-269a790cf015', path: '', url: 'http://34.16.128.64:8090/')], contextPath: null, war: '**/*.war'
            }
        }
        stage('Nexus Upload'){
            steps{
            nexusArtifactUploader artifacts: [[artifactId: 'corelogic', classifier: '', file: 'target/Test-PollSCM-Corelogic.war', type: 'war']], credentialsId: '557309c7-941c-409f-8976-b41681edcabf', groupId: 'com.adaequare', nexusUrl: '34.125.35.168:8081/', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '1.0-SNAPSHOT'
            }
        }
    }
}
