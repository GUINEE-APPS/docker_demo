pipeline {
    agent none
    stages {
        
        stage('Build') {
            agent { 
                    node {
                        label 'ubuntu'
                    } 
                }
            steps {
                checkout scm
                sh 'ls -l'
            }
        }
        stage('Deploy') {
            agent { 
                    node {
                        label 'ubuntu'
                    } 
                }
            
            steps {
                sh  """
                    docker build  -t todomarket:1.0.0 .
                    docker rm -f todomarketReact ||  true
                    docker run -dit  --name todomarketReact --env "VIRTUAL_HOST=todomarket.guineeaservice.com"  todomarket:1.0.0
               
                    """
               
            }
        }

    }
}