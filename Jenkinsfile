pipeline {
    agent { label 'windows-soa' }
<<<<<<< HEAD

=======
>>>>>>> 1ba4ae152b9df2cb52fe35e16d6448892ea2c4d4
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
