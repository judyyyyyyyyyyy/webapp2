pipeline{

    agent any

    stages{

        stage('Git Checkout'){

            steps{

                script{

                    git branch: 'devops', url: 'https://github.com/judyyyyyyyyyyy/webapp2.git'
                }
            }
        }
        stage('UNIT Testing'){
            
            steps{

                script{

                    sh 'mvn test'
                }
            }
        }
    }
}