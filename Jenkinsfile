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
    }
}