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
                 bat "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DeployBack -Dsonar.host.url=http://localhost:9000 -Dsonar.login=b56de039627e09e7e7e6ad73a7406d9f45ace85a -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/.mvn**,**/src/test/**,**/model/**,**Application.java "
                }

            }
        }
    }
}