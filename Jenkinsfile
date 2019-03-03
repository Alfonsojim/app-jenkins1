pipeline {
    agent any
    stages {
        stage ('Build') {
            steps {
                sh 'docker build -t app:test .'
            }
        }
        stage ('Test') {
            steps {
                echo 'Test de la imagen'
                sh 'docker run --rm --name app -id -p 80:80 app:test'
                sh '/bin/nc -vz localhost 80'
            }
            post {
                always{
                    sh 'docker container stop app'
                }
            }
        }
        stage ('Push Registry') {
            steps {
                withcCredentials([UsernamePassword(credentialsId: 'dockerhub', passwordVariable:'226Juma7', usernameVariable: 'harckus')]) {
                  sh 'docker tag app:test harckus/app:stable'
                  sh 'docker push harckus/app:stable '  
                }         
             
            }
        }
    }
}
