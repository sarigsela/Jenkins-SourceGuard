pipeline {
      agent any
      
      
      
     stages {
    
        stage('Clone Github repository') {
           
           steps {
             
             checkout scm
           
             }
  
          }
       
         stage('SourceGuard Code Scan') {
            
             
             steps {
                
                sh 'export SG_CLIENT_ID='SG_CLIENT_ID''
                SH  'export SG_SECRET_KEY='SG_SECRET_KEY''
               
                sh 'chmod +x sourceguard-cli'
                sh './sourceguard-cli -src .'

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
             
                 steps {
                    
              sh './sourceguard-cli -img sg.tar'

                } 
           }
   
                 
     } 
}
