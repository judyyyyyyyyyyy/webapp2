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
        stage('Integration testing'){

            steps{

                script{

                    sh 'mvn verify -DskipUnitTests'
                }
            }
        }
        /*
        stage('Static code analysis'){

            steps{

                script{
                    withSonarQubeEnv(credentialsId: 'sonarqube-api') {
                        sh 'mvn clean package sonar"sonar'
                    }
                }
            }
        }
        stage('Quality Gate status'){

            steps{

                script{

                    waitForQualityGate abortPipeline: false, credentialsId: 'sonarqube-api'

                }
            }
        }
        stage('Maven Build'){

            steps{

                script{

                    sh 'mvn clean install'
                }
            }
        }
        */
        stage('Nexus artifact upload'){

            steps{

                script{
                    nexusArtifactUploader artifacts: 
                    [[
                        artifactId: 'springboot', 
                        classifier: '', 
                        file: 'target/Uber.jar', 
                        type: 'jar'
                        ]], 
                        credentialsId: 'bc9e151d-cfc0-4f92-a7c4-10ab17c95357', 
                        groupId: 'com.example', 
                        nexusUrl: '54.198.228.108:8081', 
                        nexusVersion: 'nexus2', 
                        protocol: 'http', 
                        repository: 'maven-release', 
                        version: '2.0.0'
                }
            }
        }
    }
}