pipeline{
    
    agent any
    
    environment{
        
        registryName="cassbanadevopsrepo"
        registryUrl="cassbanadevopsrepo.azurecr.io"
        registryCredential="ACR"
        dockerImage=''
    }
    
    stages{
        stage('Checkout'){
            
            steps{
            
            checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/jaison-jack/java.git']]])
           }
        }
        stage('Build Docker Image'){
            steps{
                script{
                 dockerImage=docker.build registryName
                    
                  }
                }
             }
        stage('upload image to ACR'){
            steps{
                script{
                    docker.withRegistry("http://${registryUrl}",registryCredential){
                        dockerImage.push()
                    }
                }
            }
        }
        
            }
          }
