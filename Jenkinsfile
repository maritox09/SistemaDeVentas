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
              sh "${mvnHome}/bin/mvn -f /pom.xml verify sonar:sonar -Dsonar.login=admin -Dsonar.password=chema10"
            }
        }
     }
      stage('Quality gate') {
         def qg = waitForQualityGate()
         if (qg.status != 'OK') {
         error "Pipeline aborted due to quality gate failure: ${qg.status}"
         }else {
         echo 'Pipeline completed'
         }
      }
   }
}
