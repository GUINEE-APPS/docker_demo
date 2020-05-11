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
                    docker build  -t guineeapps_front:1.0.0 .
                    docker rm -f guineeappsReact ||  true
                    docker run -dit  --label traefik.docker.network=proxy_https_default  --label traefik.frontend.rule=Host:guineeapps.com  --label traefik.port=80  --label traefik.backend=guineeappsReact --name guineeappsReact --network  proxy_https_default  guineeapps_front:1.0.0
               
                    """
               
            }
        }

    }
}