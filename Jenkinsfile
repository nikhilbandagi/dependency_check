pipeline {

   agent any

            stages {

      stage('Git Checkout') {

         steps {

            git 'https://github.com/nikhilbandagi/mvn_sonar.git'

                        }

            }

            stage('Build') {

                        steps {

                              //withSonarQubeEnv('sonar') {

                                                sh '/opt/maven/bin/mvn clean verify sonar:sonar -Dmaven.test.skip=true'

                                    //}

                        }

            }

            // seems some issue with quality gates in latest jenkins version so commented out

            /*stage("Quality Gate") {

            steps {

              timeout(time: 2, unit: 'MINUTES') {

                waitForQualityGate abortPipeline: true

              }

            }

          } */

            stage ('Deploy') {

                        steps {

                                    sh '/opt/maven/bin/mvn clean deploy -Dmaven.test.skip=true'

                        }

            }

            stage ('Release') {

                        steps {

                                    sh 'export JENKINS_NODE_COOKIE=dontkillme ;nohup java -jar $WORKSPACE/target/*.jar &'

                        }

            }

}

}
