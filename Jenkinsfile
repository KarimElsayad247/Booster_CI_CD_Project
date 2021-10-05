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
                    docker build -t karimelsayad/django-app:dev .
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
                        
                        docker push karimelsayad247/hello-world:push-test
                    """
                    // docker push karimelsayad247/django-app:dev
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
                    docker run -d -p 8000:8000 --name dangoApp django-app:dev
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
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}
