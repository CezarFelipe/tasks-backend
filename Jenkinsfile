pipeline{
    agent any
    stages{
        stage ('Build Backend'){
            steps{
                bat 'echo Build do Backend'
                bat 'mvn clean package -DskipTests=true'
            }
        }
    }
}