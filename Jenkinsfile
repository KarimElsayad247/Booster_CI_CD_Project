pipeline{
    agent{
        label "local"
    }
    stages{
        stage("fetch"){
            steps{
                echo "========executing fetch========"
                git "https://github.com/KarimElsayad247/Booster_CI_CD_Project.git"
            }
            post{
                success{
                    echo "========fetch executed successfully========"
                }
                failure{
                    echo "========fetch execution failed========"
                }
            }
        }
        stage("docker build"){
            steps{
                echo "====++++executing docker build++++===="
                sh """
                    docker build -t karimelsayad247/django-app:prod .
                """
            }
            post{
                success{
                    echo "====++++docker build executed successfully++++===="
                }
                failure{
                    echo "====++++docker build execution failed++++===="
                }
            }
        }
        stage("docker push"){
            steps{
                echo "====++++executing docker push++++===="
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) {
                    sh """
                        docker login -u ${USERNAME} -p ${PASSWORD}
                        docker push karimelsayad247/django-app:prod
                    """
                }
            }
            post{
                success{
                    echo "====++++docker push executed successfully++++===="
                }
                failure{
                    echo "====++++docker push execution failed++++===="
                }
        
            }
        }
        stage("deploy container"){
            steps{
                echo "====++++executing deploy container++++===="
                sh """
                    docker container stop djangoApp-dev || true
                    docker container rm djangoApp-dev || true
                    docker container run -d -p 8001:8000 --name djangoApp-dev karimelsayad247/django-app:prod
                """
            }
            post{
                success{
                    echo "====++++deploy container executed successfully++++===="
                }
                failure{
                    echo "====++++deploy container execution failed++++===="
                }
        
            }
        }
    }
    post{
        success{
            echo "========pipeline executed successfully ========"
            slackSend(color: "#008800", message: "App built and deployed successfully")
        }
        failure{
            echo "========pipeline execution failed========"
            slackSend(color: "#880000", message: "${env.JOB_NAME}: Pipeline failed: ")
        }
    }
}
