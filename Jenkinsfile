pipeline {
    agent {
        node {
            label "linux && java21"
        }
    }
    stages{
        stage('Build'){
            steps{
                echo 'Hello build'
            }
        }
        stage('Test'){
            steps{
                echo 'Hello Test'
            }
        }
        stage('Deploy'){
            steps{
                echo 'Hello Deploy'
            }
        }
    }

    post {
        always{
            echo "I will always say Hello again"
        }
        success{
            echo "Yes Success"
        }
        failure{
            echo "Oh no failure"
        }
        cleanup{
            echo "Dont' care success or error"
        }
    }
        
    
}
