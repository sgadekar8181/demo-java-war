pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/sgadekar8181/demo-java-war.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn -Dmaven.test.failure.ignore=true clean package'
            }
        }
    }

    post {
        success {
            // Added allowEmptyResults so it doesn't fail when there are no tests
            junit allowEmptyResults: true, testResults: '**/target/surefire-reports/TEST-*.xml'
            
            // Archives the successfully generated .war file
            archiveArtifacts artifacts: 'target/*.war', followSymlinks: false
        }
    }
}
