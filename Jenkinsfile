pipeline {
    agent any
    
    stages {
        stage('Git Checkout') {
            steps {
                script {
                    git branch: 'main', url: 'https://github.com/Aashima-sharma/innovation-task-php.git'
                }
            }
        }
        

        
        stage('Clear space') {
           steps {
               script {
                   sh '''
                       docker rmi mysql:5.7
                       docker rmi php-mysql-demo:1.0.0
                       docker rmi phpmyadmin/phpmyadmin:4.7
                   '''
                 }
             }
        }

        stage('Build') {
            steps {
                sh "docker-compose up -d --build"
            }
        }
        
       
        stage('Tag images') {
             steps {
                 script {
                     sh '''
                         docker tag mysql:5.7 mysql:$BUILD_NUMBER
                         docker tag php-mysql-demo:1.0.0 php-mysql-demo:$BUILD_NUMBER
                         docker tag phpmyadmin/phpmyadmin:4.7 phpmyadmin/phpmyadmin:$BUILD_NUMBER
                     '''
                 }
             }
         }
    }
    
}

