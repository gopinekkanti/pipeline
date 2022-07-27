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
                    slackSend (channel: 'sonarqube', message: "Build Successful: ${env.JOB_NAME} [${env.BUILD_NUMBER}], teamDomain: 'ngroupspvtltd', tokenCredentialId: 'sona', (${env.BUILD_URL})")
            }
        }
        stage('CodeQulity'){
            steps {
            withSonarQubeEnv('SonarQube'){
            sh 'mvn clean install -f pom.xml sonar:sonar' 
              }
               slackSend (channel: 'sonarqube', message: "Code hasbeen Scanned: ${env.JOB_NAME} [${env.BUILD_NUMBER}], teamDomain: 'ngroupspvtltd', tokenCredentialId: 'sona', (${env.BUILD_URL})")

            }
        }
        stage('deploy'){
            steps{
                sshPublisher(publishers: [sshPublisherDesc(configName: 'SonarQube', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'ls', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: 'target', sourceFiles: '**/*.war')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
                slackSend (channel: 'sonarqube', message: "Deployed to $configname Successfully: ${env.JOB_NAME} [${env.BUILD_NUMBER}], teamDomain: 'ngroupspvtltd', tokenCredentialId: 'sona', (${env.BUILD_URL})")
           }
        }
        
    }
}
