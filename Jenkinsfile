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
              sh "mvn sonar:sonar"
            }
        }
     }
   }
}
