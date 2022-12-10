pipeline{
    agent{
        docker {
            image 'maven'
            args'-v $HOME/.m2:/root/.m2'
        }
    }
    stages{
        stage("Qualtiy Gate Status CHeck"){
            steps{
                script {
                    withSonarQubeEnv(credentialsId: 'SonarQube-Token')
                    sh "mv sonar:sonar"
                }
                timeout (time:1, unit: 'HOURS'){
                    def qg=waitforQualityGtae()
                     if(qg.status!= 'OK'){
                        error "Pipeline aborted due to Quality Gates failure: ${qg.status}"
                     }
                     sh "mvn claen install"
                }

            }
            }
        }
    }
    