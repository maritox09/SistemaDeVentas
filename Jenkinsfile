pipeline{
   agent any
   stages{
     stage('SCM Chekout'){
        steps{
         git 'https://github.com/maritox09/SistemaDeVenta'
        }
     }
     stage('Compile-Package'){
        steps{
         sh 'mvn package'
        }
     }
   }
}
