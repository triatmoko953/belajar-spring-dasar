pipeline {
    agent {
        node {
            label "linux && java21"
        }
    }
    stages{
        stage('Build'){
            steps{
                echo ("Hello build 1")
                echo ("Hello build 2")
                echo ("Hello build 3")
            }
        }
        stage('Test'){
            steps{
                echo ("Hello test 1")
                echo ("Hello test 2")
                echo ("Hello test 3")
            }
        }
        stage('Deploy'){
            steps{
                echo ("Hello deploy 1")
                echo ("Hello deploy 2")
                echo ("Hello deploy 3")
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
