pipeline{
    agent{
        label "local"
    }
    stages{
        stage("fetch"){
            steps{
                echo "========executing fetch========"
                git https://github.com/KarimElsayad247/Booster_CI_CD_Project.git
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
                    echo "building here"
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