pipeline {
    agent any
    stages {
        stage ('Build Backend'){
            steps {
                bat 'mvn clean package -DskipTests=true'
            }
        }
        stage ('Unit Tests'){
            steps {
                bat 'mvn test'
            }
        }
        stage ('Sonar Analysis'){
            environment {
                scannerHome = tool 'SONAR_SCANNER'
            }
            steps {
                withSonarQubeEnv('SONAR_LOCAL'){
                 bat "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DeployBack -Dsonar.host.url=http://localhost:9000 -Dsonar.login=2350eec096a3abe292723e039e94d2ac1604df31 -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/.mvn**,**/src/test/**,**/model/**,**Application.java "
                }

            }
        }
    }
}