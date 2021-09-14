pipeline{
   agent any
   tools{
      maven 'Maven'
   }
   stages{
     stage('SCM Chekout'){
        steps{
         git 'https://github.com/maritox09/SistemaDeVentas'
        }
     }
      stage('Compile-Package'){
        steps{
         sh 'mvn package'
        }
     }
     stage('SonarQube.Analysis'){
        steps{
           withSonarQubeEnv('sonarqube') {
              sh "mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=chema10"
            }
        }
     }
     stage('Deploy container'){
        steps{
           sh 'cd tests && mvn package && cd target'
           deploy adapters: [tomcat9(credentialsId: '004', path: '', url: 'http://localhost:7072/')], contextPath: 'rps', war: '*/.war'
        }
     }
   }
}
