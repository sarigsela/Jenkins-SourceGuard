pipeline {
      agent any
      environment {
           SG_CLIENT_ID = credentials("SG_CLIENT_ID")
           SG_SECRET_KEY = credentials("SG_SECRET_KEY")
      
        }
     stages {
    
        stage('Clone Github repository') {
           
           steps {
             
             checkout scm
           
             }
  
          }
       
         stage('SourceGuard Code Scan') {
            
              agent {

              docker { image 'sourceguard/sourceguard-cli' }

              }

             steps {
               
               
              
                sh "/sourceguard-cli -src ./"

                } 
          }

         
         
       stage('Docker image Build') {
           
            
             
             steps{

              sh 'docker build -t dhouari/sg .'
             
              
              }
             
           }
        
       stage('Docker image prep') {
           
             
             
             steps{

              sh 'docker save dhouari/sg -o sg.tar'
             
              
              }
             
           }
           stage('Docker image scan') {
                agent {

                   docker { image 'sourceguard/sourceguard-cli:latest' }

                    }

                 steps {
                    
                     sh "/sourceguard-cli -img sg.tar/"

                   } 
             }
   
                 
     } 
}
