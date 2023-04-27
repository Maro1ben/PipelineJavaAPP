pipeline {
    agent any

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "M3"
    }

    stages {
        stage('GIT') {
            steps {
                // Get some code from a GitHub repository
                git url :  'https://github.com/matthcol/movieapp_jdbc.git',
                    branch: 'main'
        }
        stage('COMPILE'){
            steps{
                sh "mvn clean compile"
            }
        }
        stage('TEST'){
            steps{
                sh "mvn test"
            }
            post{
                always {
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
            }
        }
        stage('PACKAGE'){
            steps{
                sh "mvn test -DskipTests -Dmaven.test.skip package"
            }
            post {
                success {
                    archiveArtifacts 'target/*.jar'
                }

            }

        }
    }
}
}