pipeline {
    agent any
    stages {
        stage('Clean') {
            steps {
                deleteDir()
            }
        }
        stage('Build') {
            steps {
                // Get some code from a GitHub repository
                git 'https://github.com/nlilaramani/Calc.git'
                //withMaven(maven: 'MAVEN_HOME'){
                    sh "mvn -Dmaven.test.failure.ignore=true clean package"    
                //}
                // Run Maven on a Windows agent.
                //sh "mvn -Dmaven.test.failure.ignore=true clean package"

                // To run Maven on a Unix agent, use
                // sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }
            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                //added some comment
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}
