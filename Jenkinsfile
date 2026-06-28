pipeline {
    agent none

    environment{
        AUTHOR = "Tri Atmoko"
        EMAIL = "moko@gmail.com"
    }

    //triggers{
        // cron("*/5 * * * *")
    //}

    parameters{
        string(name: "NAME", defaultValue: "Guest", description: "What is your name?")
        text(name: "DESCRIPTION", defaultValue: "Guest", description: "Tell me about you")
        booleanParam(name: "DEPLOY", defaultValue: false, description: "Need To Deploy?")
        choice(name: "SOCIAL_MEDIA", choices : ['Instagram','FaceBook','Twitter'], description: "Which social media")
        password(name: "SECRET", defaultValue: "", description: "Encrypt Key")
    }
    
    options{
        disableConcurrentBuilds()
        timeout(time: 10, unit: 'MINUTES')
    }

    stages {

        stage("OS Setup"){
            matrix{
                axes{
                    axis{
                        name "OS"
                        values "linux", "windows", "mac"
                    }
                    axis{
                        name "ARC"
                        values "32", "64"
                    }
                }
            }
            stages{
                stage("OS Setup"){
                    agent {
                        node {
                            label "linux && java17"
                        }
                    }
                    steps{
                        echo ("Setup ${OS} ${ARC}")
                    }
                }
            }
        }

        stage("Preparation"){
            parallel{
                stage("Prepare Java"){
                    agent {
                        node {
                            label "linux && java17"
                        }
                    }
                    steps{
                        echo("Prepare Java")
                        sleep(2)
                    }
                }
                stage("Prepare Maven"){
                    agent {
                        node {
                            label "linux && java17"
                        }
                    }
                    steps{
                        echo("Prepare Maven")
                        sleep(2)
                    }
                }
            }
        }

        stage("parameter"){
            agent {
                node {
                    label "linux && java17"
                }
            }
            steps{
                echo "Hello ${params.NAME}!"
                echo "You description is  ${params.DESCRIPTION}!"
                echo "Your social media is ${params.SOCIAL_MEDIA} user!"
                echo "Need to deploy : ${params.DEPLOY} to deploy !"
                echo "You secret is ${params.SECRET}"
            }
        }

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
                sh('echo "App Password : $APP_PSW" > "rahasia.txt"')
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
            input {
                message "Can we deploy?"
                ok "Yes, of course"
                submitter "trmk,moko"
                parameters {
                    choice(name: "TARGET_ENV", choices: ['DEV','QA','PROD'], description: "Which Environment?")
                }
            }
            agent {
                node {
                    label "linux && java17"
                }
            }
            steps {
                echo("Deploy to ${TARGET_ENV}")
            }
        }

        stage('Release'){
            when{
                expression{
                    return params.DEPLOY
                }
            }
            agent {
                node {
                    label "linux && java17"
                }
            }
            steps {
                echo("Release it")
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
