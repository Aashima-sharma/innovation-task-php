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
  
        

        stage('Build') {
            steps {
                sh "docker-compose up -d --build"
            }
        }
        
        
        stage('Tag images and remove old ones') {
            steps {
                script {
                    // Tag images
                    sh '''
                        docker tag mysql:5.7 mysql:$BUILD_NUMBER
                        docker tag php-mysql-demo:1.0.0 php-mysql-demo:$BUILD_NUMBER
                        docker tag phpmyadmin/phpmyadmin:4.7 phpmyadmin/phpmyadmin:$BUILD_NUMBER
                    '''

                    // Remove old images
                    sh '''
                        docker images | grep -v $BUILD_NUMBER | awk '{if ($1 ~ /^(mysql|php-mysql-demo|phpmyadmin\\/phpmyadmin)$/) print $1":"$2}' | xargs -r docker rmi -f
                    '''
                }
            }
        }
    }
}
