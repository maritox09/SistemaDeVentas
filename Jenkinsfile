def fallo = ''
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
           script{
              fallo=env.STAGE_NAME
              echo "Repositorio"
           }
           withSonarQubeEnv('sonarqube') {
              sh "mvn sonar:sonar -Dsonar.login=admin -Dsonar.password=chema10"
            }
        }
     }
     stage("Quality Gate"){
        steps {
            script {
                fallo=env.STAGE_NAME
                echo "Quality Gate"
                timeout(time: 1, unit: 'HOURS') {
                   def qg = waitForQualityGate()
                   if (qg.status != 'OK') {
                     error "Pipeline aborted due to quality gate failure: ${qg.status}"
                   }
                 }
            }
         }
     } 
     stage('Deploy container'){
        steps{
           sh 'cd target'
           deploy adapters: [tomcat9(credentialsId: '999', path: '', url: 'http://192.168.5.194:7072/')], contextPath: 'rps', war: '**/*.war'
        }
     }
   }
   post{
      failure{
         mail bcc: '',
            body: "Project: ${currentBuild.currentResult} Job: ${env.JOB_NAME} URL: ${env.BUILD_URL} Buil Number: ${env.BUILD_NUMBER} Fallo: ${fallo}", 
            cc: '', 
            from: '', replyTo: '',
            subject: 'Pipeline fail', 
            to: 'jmyc9999@gmail.com'
      }
   }
}
