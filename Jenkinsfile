pipeline {
    agent { dockerfile true }
    options {
        skipStagesAfterUnstable()
    }
    tools { 
        maven 'Maven 3.8.2' 
        jdk 'jdk 1.8.0_302' 
    }
    
    environment {
      DOCKER_CERT_PATH = credentials('docker_id')
    }
    stages {
        stage ('Initialize') {
            steps {
                sh '''
                    echo "PATH = ${PATH}"
                    echo "M2_HOME = ${M2_HOME}"
                '''
            }
        }
        stage('build') {
            steps {
                sh 'mvn -Dmaven.test.failure.ignore=true install' 
                echo ' testing build success. '
            }
        }
        stage('Sanity check') {
            steps {
                input "Does the staging environment look ok?"
            }
        }
        
        stage('test') {
            steps {
                echo ' testing success.******* '
            }
        }
    }
    /*post {
        always {
            echo 'One way or another, I have finished'
            //deleteDir()
        }
        success {
            echo 'I succeeded!'
        }
        unstable {
            echo 'I am unstable :/'
        }
        failure {
            echo 'I failed :('
        }
        changed {
            echo 'Things were different before...'
        }
    }*/
}
