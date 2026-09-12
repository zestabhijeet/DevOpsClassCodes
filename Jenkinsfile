
pipeline{
    tools{
        jdk 'myjava'
        maven 'mymaven'
    }
	agent any
      stages{
           stage('Checkout'){
	    
               steps{
		 echo 'cloning..'
                 git 'https://github.com/zestabhijeet/DevOpsClassCodes.git'
              }
          }
          stage('Compile'){
             
              steps{
                  echo 'compiling..'
                  sh 'mvn compile'
	      }
          }
          stage('CodeReview'){
		  
              steps{
		    
		  echo 'codeReview'
                  sh 'mvn pmd:pmd'
              }
          }
           stage('UnitTest'){
		  
              steps{
	         echo 'Testing'
                  sh 'mvn test'
              }
               post {
               success {
                   junit 'target/surefire-reports/*.xml'
               }
           }	
          }
           stage('Coverage'){
              
              steps{
                  echo 'generating coverage report'
                  sh 'mvn jacoco:prepare-agent test jacoco:report'
              }
              
          }
          stage('SonarCloud Analysis'){
 
              steps{
                  echo 'running sonar analysis'
                  withCredentials([string(credentialsId: 'sonarcloudtoken', variable: 'SONAR_TOKEN')]) {
                      sh 'mvn sonar:sonar -Dsonar.organization=zestabhijeet -Dsonar.projectKey=REPLACE_WITH_PROJECT_KEY -Dsonar.host.url=https://sonarcloud.io -Dsonar.token=$SONAR_TOKEN'
                  }
              }
          }
          stage('Package'){
		  
              steps{
		  
                  sh 'mvn package'
              }
          }
	     
          
      }
}
 
