pipeline{
    agent any
    
    
    stages{
        
        stage('Cleaning the project') {
            steps{
                sh "npm ci  " 
            }
        }
        
        
        
        
        
        stage('Artifact Construction') {
            steps{
                sh "ng build  " 
            }
        }
        
         
        
     
      
          stage('Build Docker Image') {
                      steps {
                          script {
                            sh 'docker build -t anissaidi/angular-app .'
                          }
                      }
                  }
        
        stage('Docker login') {
                      steps {
                          script {
                        
                              sh 'docker login -u anissaidi -p anisaziz50'}
                      }
                      }
                stage('Pushing Docker Image') {
                      steps {
                          script {
                           
                           sh 'docker push anissaidi/angular-app'
                          }
                      }
                }
                 
        
        stage('Run Angular Container') {
                      steps {
                          script {
                            sh 'docker-compose up -d'
                          }
                      }
                  }
                  
                  stage('Launch Angular in browser') {
                    steps {
                          script {
                           
                            sh 'python3 -mwebbrowser http://localhost:80/product '
                          }
                    }
                  }
            

    }  
   
}
       
