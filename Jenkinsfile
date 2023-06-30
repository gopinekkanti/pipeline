pipeline {
    agent any
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
