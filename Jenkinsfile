pipeline{
    agent {
       docker { 
           image 'trion/ng-cli' 
       }     
    }
    stages {
        stage('Checkout') { 
         agent any 
          steps { 
               deleteDir() 
               checkout scm 
          } 
       } 
        stage('Install Node Module'){
           steps { 
               sh 'npm install'  
           }    
        }
        stage('Test'){
            steps { 
                echo "Testing..."
           } 
        }
        stage('Build'){
            steps { 
               sh 'ng build' 
               sh 'ls' 
               
            } 
        }
         stage('Archive'){
            steps { 
               sh 'tar -cvzf ng_project.tar.gz --strip-components=1 dist' 
               archive 'ng_project.tar.gz'
               
            } 
        }
        
        stage('Nexus') {
            agent none 
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS' 
              }
            }
           
            steps {
               sh 'echo Stage 1'
            }
        } 
    }
}
