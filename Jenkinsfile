pipeline {
    agent { label 'windows-soa' }
    environment {
        SOA_ANT_HOME='C:/Oracle/Middleware/Oracle_Home/soa/bin'
    }

    stages {
        stage('Package SOA Composites') {
            
            steps {
                bat 'ant -version'
                bat 'java -version'
                bat "cd /d "${env.SOA_ANT_HOME}"
                bat 'ant -f build.xml package-all'
            }
        }
        stage('Archive Artifacts') {
            steps {
                bat 'copy "%WORKSPACE%\\SOA\\deploy\\*.jar" "D:\\"'
            }
        }
    }

    post {
        success {
            echo 'Packaging completed successfully.'
        }
        failure {
            echo 'Packaging failed.'
        }
    }
}
