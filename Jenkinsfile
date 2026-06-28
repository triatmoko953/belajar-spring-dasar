pipeline {
    agent none

    environment{
        AUTHOR = "Tri Atmoko"
        EMAIL = "moko@gmail.com"
    }

    stages {

        stage('Prepare') {
            environment {
                APP = credentials("moko_rahasia")
            }
            agent {
                node {
                    label "linux && java17"
                }
            }
            steps {
                echo("Author : ${AUTHOR}")
                echo("App User : ${APP_USR}")
                echo("App Password : ${APP_PSW}")
                echo("Author : ${EMAIL}")
                echo("Start Job : ${env.JOB_NAME}")
                echo("Start Build : ${env.BUILD_NUMBER}")
                echo("Branch Name : ${env.BRANCH_NAME}")
            }
        }

        stage('Build') {
            agent {
                node {
                    label "linux && java17"
                }
            }
            steps {
                script {
                    for (int i = 0; i < 10; i++) {
                        echo("Script ${i}")
                    }
                }

                echo("Start Build")
                sh("./mvnw clean compile test-compile -X")
                echo("Finish Build")
            }
        }

        stage('Test') {
            agent {
                node {
                    label "linux && java17"
                }
            }
            steps {
                script {
                    def data = [
                        "firstName": "Tri",
                        "lastName" : "Atmoko"
                    ]

                    writeJSON(file: "data.json", json: data)
                }

                echo("Start Test")
                sh("./mvnw test")
                echo("Finish Test")
            }
        }

        stage('Deploy') {
            agent {
                node {
                    label "linux && java17"
                }
            }
            steps {
                echo("Hello deploy 1")
                sleep(2)
                echo("Hello deploy 2")
                echo("Hello deploy 3")
            }
        }
    }

    post {
        always {
            echo "I will always say Hello again"
        }

        success {
            echo "Yes Success"
        }

        failure {
            echo "Oh no failure"
        }

        cleanup {
            echo "Dont' care success or error"
        }
    }
}
