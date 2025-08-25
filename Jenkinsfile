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
                bat "cd /d \"${env.SOA_ANT_HOME}\" && ant -f build.xml package-all"
            }
        }
        stage('Archive Artifacts') {
            steps {
                bat 'copy "%WORKSPACE%\\SOA\\deploy\\*.jar" "D:\\"'
            }
        }
        stage('deploy SOA Composites') {
            steps {
                withCredentials([string(credentialsId: 'USER_PWD', variable: 'weblogic_pwd')]) {
                    bat "cd /d \"${env.SOA_ANT_HOME}\" && ant -f build.xml deploy-all -DUSER_PWD=${weblogic_pwd}"
                }
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
