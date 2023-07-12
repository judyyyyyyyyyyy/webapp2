pipeline{

    agent any

    parameters{

        string(name: 'region', defaultValue: 'us-east-1', description: 'Choose AWS Region')
    }

    environment{

        ACCESS_KEY = credentials('AWS_ACCESS_KEY_ID')
        SECRET_KEY = credentials('AWS_SECRET_KEY_ID')
    }

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
        
        stage('Nexus artifact upload'){

            steps{

                script{

                    def readPomVersion = readMavenPom file: 'pom.xml'
                    def nexusRepo = readPomVersion.version.endsWith("SNAPSHOT") ? "maven-snapshot" : "maven-release"

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
                        nexusVersion: 'nexus3', 
                        protocol: 'http', 
                        repository: nexusRepo, 
                        version: "'${readPomVersion.version}"
                }
            }
        }
        */
        stage('docker image build'){
            steps{
                script{

                    sh """
                    aws configure set aws_access_key_id "$ACCESS_KEY"
                    aws configure set aws_secret_key_id "$SECRET_KEY"
                    aws configure set region "${params.region}"
                    aws ecr get-login-password --region ${params.region} | docker login --username AWS --password-stdin 996864587356.dkr.ecr.${params.region}.amazonaws.com
                    docker build -t webapp .
                    docker tag webapp:latest 996864587356.dkr.ecr.${params.region}.amazonaws.com/webapp:latest
                    docker push 996864587356.dkr.ecr.${params.region}.amazonaws.com/webapp:latest
                    """
                }
            }
        }
    }
}