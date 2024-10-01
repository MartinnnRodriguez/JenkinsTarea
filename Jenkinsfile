pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building...'
            }
        }

        stage('Test') {
            steps {
                echo 'Testing...'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deploying Nginx server...'
                
                // Detener y eliminar el contenedor si ya existe
                sh '''
                    docker stop mi-nginx-server || true
                    docker rm mi-nginx-server || true
                '''
                
                // Levantar el contenedor de Nginx
                sh 'docker run -d -p 8081:80 --name mi-nginx-server nginx'
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
            // Mostrar el estado de los contenedores
            sh 'docker ps -a'
            // Mostrar logs del contenedor
            sh 'docker logs mi-nginx-server || true'
        }
    }
}
