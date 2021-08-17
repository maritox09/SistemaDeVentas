pipeline{
   stage('SCM Chekout'){
     git 'https://github.com/maritox09/SistemaDeVenta'
   }
   stage('Compile-Package'){
     sh 'mvn package'
   }
}
