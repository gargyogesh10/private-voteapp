pipeline{
    agent any
    options { 
        buildDiscarder(logRotator(numToKeepStr: '15'))
        disableConcurrentBuilds()
        retry(2)
        timeout(time: 20, unit: 'MINUTES') 
    }
    parameters {
        string(name: 'BRANCH', defaultValue: 'main', description: 'branch to build?')
        choice(name: 'ENV', choices: ['qa', 'dev', 'prod'], description: 'env to build')
    }
    stages{
        stage("Docker login and push"){
            steps{
                sh "docker login -u yogesh010 -p Upgrad@123"           
                sh '''
                    cd vote
                    docker build -t yogesh010/vote:v${BUILD_NUMBER} .
                    '''
                sh "docker push yogesh010/vote:v${BUILD_NUMBER}"
            }
        }
        stage("Test"){
            steps{
                sh "echo linux test"
                sh "sleep 180"
            }
        }
        stage("Test2"){
            steps{
                sh "echo window test"
                sh "sleep 180"
            }
        }
        stage("deploy"){
            steps{
                sh "echo starting deployment"
            }
        }
    }
}
