pipeline {
 
    agent { node { label 'rhea' } }

    stages {
                                     
        stage('cleanup docker system') {

            steps {

                dir('.build-automation/docker-image-management') {

                    sh 'bash ./cleanup-local-docker-system.bash'
                    
                }                

            }

        }   

        stage('build docker image') {

            steps {

                dir('.build-automation/docker-image-management') {

                    sh 'bash ./build-docker-image-from-source.bash'

                }                

            }

        }      
        
        stage('push to dockerhub') {

            steps {

                dir('.build-automation/docker-image-management') {

                    sh 'bash ./push-docker-image-to-dockerhub.bash'

                }                

            }

        }

        stage('deploy container') {

            steps {

                dir('.build-automation/local-execution-management') {

                    sh 'bash ./deploy-latest-docker-image-localhost.bash'

                }                

            }

        }

        stage('monitor deployments') {

            steps {

                dir('.build-automation/local-execution-management') {

                    sh 'bash ./display-container-usage.bash'

                }                

            }

        }
        
        stage('cleanup docker again') {

            steps {

                dir('.build-automation/docker-image-management') {

                    sh 'bash ./cleanup-local-docker-system.bash'

                }                 

            }

        }
        
}}