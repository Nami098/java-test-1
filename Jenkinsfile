pipeline {
    
    agent {
        docker { image 'maven:3.3.3' }
    }
    stages {
        stage('mvn-build') {
            steps {
                sh 'mvn --version'
                sh 'mvn clean install'
                
            }
        }
    }
}
