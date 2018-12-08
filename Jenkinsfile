node{
    //checkout git repository (master branch)
    stage('checkout'){
        checkout scm
    }

    //maven build
    stage('build'){
        dir('b2bGinebra/'){
            sh 'mvn clean package' 
        }  
    }

    //deployment in docker
    stage('deployment'){
        dir('deployment/'){
             sh 'docker-compose stop' //stop existing containers
             sh 'docker-compose rm -f' //remove existing containers
             sh 'docker volume rm deployment_pg_data' //remove database volume, remove this part in production
             sh 'docker-compose up -d --build' //redeploy containers
             sh 'docker rmi $(docker images -f dangling=true -q)' //remove unused images
        }
    }
}