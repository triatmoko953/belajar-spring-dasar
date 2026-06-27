pipeline {
    agent {
        node {
            label "linux && java17"
        }
    }
    stages{
        stage('Build'){
            steps{
                script{
                    for (int i = 0; i < 10; i++){
                        echo("Script ${i}")
                    }
                }
                echo("Start Build")
                sh("./mvnw clean compile test-compile -X")
                echo("Finish Build")
            }
        }
        stage('Test'){
            steps{
                echo("Start Test")
                sh("./mvnw test")
                echo("Finish Test")
            }
        }
        stage('Deploy'){
            steps{
                echo ("Hello deploy 1")
                sleep(2)
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
