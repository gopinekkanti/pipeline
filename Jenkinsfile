pipeline {
    agent any
    stages {
        stage('checkout') {
            steps {
git branch: 'main', url: 'https://github.com/gopinekkanti/pipeline.git'           
            }
        }
        stage('build'){
            steps{
                sh 'mvn clean install -f pom.xml'            
            }
        }
        stage('CodeQulity'){
            steps {
            withSonarQubeEnv('sonarjenkins'){
            sh 'mvn clean install -f pom.xml sonar:sonar' 
              }
}
}
    }
}
