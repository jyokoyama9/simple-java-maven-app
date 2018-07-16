pipeline { 
   agent {
       docker {
           image 'maven:3.5.4-jdk-8'
           args '-v ${WORKSPACE}/.m2:/root/.m2' 
       }
   }
    stages { 
        stage('Build') { 
            steps { 
                sh 'mvn -Dmaven.test.failure.ignore=true clean test package site' 
            }
            post {
                success {
                    archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
                    junit 'target/surefire-reports/**/*.xml' 
                }
            }
        }
        stage('静的解析') {
            steps {
                checkstyle 'target/checkstyle/*.xml'
            }
        }
    }
}
