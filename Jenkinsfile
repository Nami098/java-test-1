def dockerRun ='docker run -p 8080:8080 -d --name java-test namiducker/java-test:2.0.0 .'
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
                
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL}"
                echo "Workspace is ${env.WORKSPACE} and build_url is ${env.BUILD_URL}"
                sh 'mvn clean install'
                
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
        stage ('Run container on dev server'){
            steps {
                
                sshagent(['centosprivatekey']) {
                   
                    sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.3.215 ${dockerRun}"
                }
                
            }
            
        }
    }
}
