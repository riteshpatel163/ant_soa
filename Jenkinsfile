pipeline {
    agent { label 'windows-soa' }
    environment {
        SOA_ANT_HOME='C:/Oracle/Middleware/Oracle_Home/soa/bin'
        SONAR_SCANNER_HOME = tool "sonarscanner"
        SONAR_HOST = "http://master.local:9000"
        SONAR_TOKEN = credentials('sonar')  
    }

    stages {
        stage('Package SOA Composites') {
            
            steps {
                bat 'ant -version'
                bat 'java -version'
                bat "cd /d \"${env.SOA_ANT_HOME}\" && ant -f build.xml package-all"
            }
        }
        stage('sonar analysis'){
            steps{
                withCredentials([string(credentialsId: 'sonar', variable: 'SONAR_TOKEN')]){
                sh """
                ${SONAR_SCANNER_HOME}/bin/sonar-scanner \
                    -Dsonar.projectKey=soa-factorial \
                    -Dsonar.sources=src \
                    -Dsonar.host.url=${SONAR_HOST} \
                    -Dsonar.login=${SONAR_TOKEN}
                """
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
                    bat """
                    cd /d "\"${env.SOA_ANT_HOME}\" 
                    ant -f build.xml deploy-all -DserverURL=http://localhost:7001 -DUSER_PWD=${weblogic_pwd}
                    ant -f ant-sca-mgmt.xml listCompositesInPartition -Dpartition=default
                    """
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
