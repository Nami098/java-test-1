pipeline {
    
    agent any //{
        //dockerfile true
    //}
    stages {
        stage('mvn-build') {
            //agent {
            //docker { image 'maven:3.3.3' }
        //}
            steps {
                echo 'builng '
                //sh 'mvn clean install'
                
            }
        }
        stage ('Build Docker Image'){
            steps {
                sh 'docker build -t namiducker/java-test:2.0.0 .'
            }
            
        }
        stage ('Push Docker Image'){
            
            steps {
                withCredentials([string(credentialsId: 'duckerhub-pwd', variable: 'dockerhubP')]) {
                    sh "docker login -u namiducker -p ${dockerhubP}"
                }
                sh 'docker push namiducker/java-test:2.0.0'
            }
            
        }
    }
}
