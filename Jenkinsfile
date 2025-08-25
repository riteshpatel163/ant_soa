pipeline {
    agent { label 'windows-soa' }
    environment {
        ORACLE_HOME = 'C:\Oracle\Middleware\Oracle_Home'
        PATH = "${env.PATH};${env.ORACLE_HOME}/soa/bin"

    }
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
        post {
            success {
                echo 'Packaging completed successfully.'
            }
            failure {
                echo 'Packaging failed.'
            }
        }
    }
}
