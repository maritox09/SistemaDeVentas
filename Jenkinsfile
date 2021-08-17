pipeline{
   agent any
   tools{
      maven 'mvn'
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
   }
}
