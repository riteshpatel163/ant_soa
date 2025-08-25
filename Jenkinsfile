pipeline {
    agent { label 'windows-soa' }
    stages {
        stage('Package SOA Composites') {
            steps {
               bat 'ant --version'
               bat 'java -version'
               bat 'ant -f build.xml package-all'
            }
        }
        stage('Archive Artifacts') {
            steps {
                bat 'copy C:\\Users\\kumar\\Downloads\\factorial\\SOA\\deploy\\*.jar  D:'
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
