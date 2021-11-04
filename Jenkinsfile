pipeline { 

    environment { 

        registry = "aymenca/aymenca/doc" 

        registryCredential = 'aymenca' 

        dockerImage = '' 

    }

    agent any 

    stages { 

        
        
        
           stage( 'Checkout  GIT' ){
                       steps{
                           
                           echo 'Pulling ... ';
                              git branch:  'main' ,
                         
                              url :'https://github.com/faresmalleh/fares'
                              }
                    }
        stage('Cloning our Git') { 

            steps { 

                git 'https://github.com/faresmalleh/fares' 

            }

        } 

        stage('Building our image') { 

            steps { 

                script { 

                    dockerImage = docker.build registry + ":$BUILD_NUMBER" 

                }

            } 

        }

        stage('Deploy our image') { 

            steps { 

                script { 

                    docker.withRegistry( '', registryCredential ) { 

                        dockerImage.push() 

                    }

                } 

            }

        } 

        stage('Cleaning up') { 

            steps { 

                sh "docker rmi $registry:$BUILD_NUMBER" 

            }

        } 

    }

}
