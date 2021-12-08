pipeline{
    agent any
    stages{
        stage ('Build Backend'){
            steps{
                bat 'echo Build do Backend'
                bat 'mvn clean package -DskipTests=true'
            }
        }
        stage ('Unit Tests'){
            steps{
                bat 'echo Unit Tests'
                bat 'mvn test'
            }
        }
        stage ('Sonar Analysis'){
            environment{
                scannerHome = tool 'SONAR_SCANNER'
            }
            steps{
                bat 'echo Sonar Analysis'
                withSonarQubeEnv ('SONAR_LOCAL'){
                    bat "${scannerHome}/bin/sonar-scanner -e -Dsonar.projectKey=DeployBack -Dsonar.host.url=http://localhost:9000 -Dsonar.login=0141b0033ba4fa66f576e3937c543cb17fcc4878 -Dsonar.java.binaries=target -Dsonar.coverage.exclusions=**/.mvn/**,**/src/test/**,**/model/**,**Aplication.java,**/src/main/java/br/ce/wcaquino/taskbackend/utils/ValidationException.java,src/main/java/br/ce/wcaquino/taskbackend/controller/TaskController.java,src/main/java/br/ce/wcaquino/taskbackend/TaskBackendApplication.java,src/main/java/br/ce/wcaquino/taskbackend/controller/RootController.java"
                }
            }
        }
        stage ('Quality Gate'){
            steps{
                sleep(50)
                timeout(time: 1, unit: 'MINUTES'){
                    waitForQualityGate abortPipeline: true
                }
            }
        }
        stage ('Deploy Server Application'){
            steps{
                bat 'echo Deploy Tomcat'
                deploy adapters: [tomcat8(credentialsId: 'tomcat_login', path: '', url: 'http://localhost:8001/')], contextPath: 'tasks-backend', war: 'target/tasks-backend.war'
            }
        }
    }
}

