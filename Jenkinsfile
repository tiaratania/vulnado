pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                // Checkout the primary repository
                checkout([$class: 'GitSCM', branches: [[name: '*/main']],
                          userRemoteConfigs: [[url: 'https://github.com/tiaratania/vulnado.git']]])
                // Checkout the Jenkinsfile from another repo
                dir('jenkins-setup') {
                    git url: 'https://github.com/tiaratania/jenkins-php-selenium-test.git'
                }
            }
        }
        stage('Build') {
            steps {
                // Run the pipeline defined in the Jenkinsfile from another repo
                load 'jenkins-setup/Jenkinsfile'
            }
        }
    }
}
