pipeline{
  agent any 
  tools {
    maven "maven3.8.6"
  }  
  stages {
    stage('1GetCode'){
      steps{
        sh "echo 'cloning the latest application version' "
        git credentialsId: 'Github-credential', url: 'https://github.com/signal2009/Boa_Application'
      }
    }
    stage('3Test+Build'){
      steps{
        sh "echo 'running JUnit-test-cases' "
        sh "echo 'testing must passed to create artifacts ' "
        sh "mvn clean package"
      }
    }
    stage('4CodeQuality'){
      steps{
        sh "echo 'Perfoming CodeQualityAnalysis' "
        sh "mvn sonar:sonar"
      }
    } 
    stage('5uploadNexus'){
      steps{
        sh "mvn deploy"
      }
    }  
    stage('8deploy2prod'){
      steps{
        deploy adapters: [tomcat9(credentialsId: 'dominion-user', path: '', url: 'http://3.133.237.56:8080/')], contextPath: null, war: 'target/*war'
     }
    } 
  }
   post{
    always{
      emailext body: '''Hey guys
      Please check build status.
	  
      Thanks
      Landmark 
      +1 437 215 2483''', recipientProviders: [buildUser(), developers()], subject: 'success', to: 'folashayoomolabi@gmail.com'
    }
    success{
      emailext body: '''Hey guys
    Good job build and deployment is successful.

    Thanks
    Landmark 
    +1 437 215 2483''', recipientProviders: [buildUser(), developers()], subject: 'success', to: 'folashayoomolabi@gmail.com'
    } 
    failure{
      emailext body: '''Hey guys
    Build failed. Please resolve issues.
    Thanks
    Landmark   
    +1 437 215 2483''', recipientProviders: [buildUser(), developers()], subject: 'success', to: 'folashayoomolabi@gmail.com'
    }
  }  
 }
   
