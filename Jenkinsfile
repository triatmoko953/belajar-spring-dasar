pipeline {
    agent {
        node {
            label "linux && java21"
        }
    }
    stages{
        stage('Hello'){
            steps{
                echo 'Hello World'
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
