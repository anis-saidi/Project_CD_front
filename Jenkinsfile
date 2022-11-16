pipeline{
    agent any
    tools {
        maven 'MAVEN'}
    

    stages {
        stage('Getting project from Git') {
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], browser: [$class: 'GithubWeb', repoUrl: 'https://github.com/hassenbm88/hassenbm88-Angular_CICD_Academic_Project_Front.git'], extensions: [], userRemoteConfigs: [[credentialsId: '18558545-93a9-448f-bf74-85184c601676', url: 'https://github.com/hassenbm88/hassenbm88-Angular_CICD_Academic_Project_Front.git']]])
            }
        }
        
        
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
                            sh 'docker build -t hsounabm/angular-app .'
                          }
                      }
                  }
                  stage('Push Docker Image') {
                      steps {
                          script {
                           withCredentials([string(credentialsId: 'hsounabm', variable: 'dockerhubpwd')]) {
                              sh 'docker login -u hsounabm -p ${dockerhubpwd}'
                           }
                           sh 'docker push hsounabm/angular-app'
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
                           
                            sh 'python3 -mwebbrowser http://localhost:4200/product '
                          }
                    }
                  }
            
} 
    
   
}
       
