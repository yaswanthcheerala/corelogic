



pipeline{
    agent any
    tools{
        maven 'maven-3.8.7'
    }
    stages{
        stage('Git CHeckout'){
            steps{
                checkout scmGit(branches: [[name: 'master']], extensions: [], userRemoteConfigs: [[credentialsId: '37034ef7-c975-4cda-8cd7-4aa35baabfa6', url: 'https://github.com/PMFayazAhmed/corelogic.git']])
            }
            
        }
                stage('Build'){
            steps{
            sh 'mvn package -f pom.xml'    
            }
            
        }
        stage('Tomcat Deploy'){
            steps{
               deploy adapters: [tomcat9(credentialsId: '052a82c1-032a-4471-a551-78b14c0be15f', path: '', url: 'http://34.124.148.120:8090/')], contextPath: null, war: '**/*.war' 
            }
            
        }
        stage('Nexus Upload'){
            steps{
               nexusArtifactUploader artifacts: [[artifactId: 'corelogic', classifier: '', file: 'target/Master-Corelogic.war', type: 'war']], credentialsId: '3706baec-282e-4181-88a8-ae798531403f', groupId: 'com.adaequare', nexusUrl: '34.16.128.152:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '1.0-SNAPSHOT' 
            }
            
        }

        
    }
}
