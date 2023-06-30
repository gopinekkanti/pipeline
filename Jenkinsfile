pipeline {
    agent any
    tools {
        maven 'Maven3.8.6'
    }
    stages {
        stage('checkout') {
            steps {
                checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/gopinekkanti/pipeline.git']]])
            }
        }
        stage('build'){
            steps{
                sh 'mvn clean install -f pom.xml'            
            }
        }
}
}
