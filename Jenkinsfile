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
      stage("SonarQube"){
         withSonarQubeEnv('SonarQube') {
            sh 'cd tests && mvn clean verify sonar:sonar -Dsonar.login=admin -Dsonar.password=chema10'
         }
      }
      stage("Quality Gate") {
         timeout(time: 1, unit: 'HOURS') {
         waitForQualityGate abortPipeline: true
         }
      }
   }
}