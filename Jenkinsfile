pipeline{
     agent any
       tools{
maven 'Maven-3.8.6'
}
  stages{
   stage('Git Chckout'){
    steps{
       checkout([$class: 'GitSCM', branches: [[name: 'master']], extensions: [], userRemoteConfigs: [[credentialsId: 'a61c4eb6-96d0-4169-823d-321e65db8e98', url: 'https://github.com/PMFayazAhmed/corelogic.git']]]) 
    }   
   }
      stage('Build'){
    steps{
        sh 'mvn package -f pom.xml'
    }   
       
   }
      stage('Upload to Nexus'){
    steps{
        nexusArtifactUploader artifacts: [[artifactId: 'corelogic', classifier: '', file: 'target/PollSCM-Corelogic.war', type: 'war']], credentialsId: 'f3cae16c-a92f-4615-a198-bda3b71eae75', groupId: 'com.adaequare', nexusUrl: '34.132.95.253:8081/', nexusVersion: 'nexus3', protocol: 'http', repository: 'maven-snapshots', version: '1.0-SNAPSHOT'
    }   
       
   }
   stage('Deployment into Tomcat'){
    steps{
      deploy adapters: [tomcat9(credentialsId: '9880de70-e4ec-4e73-843e-a13eadb0c8d1', path: '', url: 'http://34.132.95.253:8080/')], contextPath: null, war: '**/*.war'  
    }   
       
   }
  }
}
