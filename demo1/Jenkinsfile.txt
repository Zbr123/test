pippipeline {
   agent any
   stages {
   stage ('one') {
         steps {
                echo  'Hi, this is ahmed'
         }
        }
        stage ('two') {
         steps {
                input ('Do you want to proceed?')
         }
        }
        stage ('Three') {
         when {
                not {
                     branch "master"
                     }
                     }
                 steps {
                        echo "Hello"
                        }
                    }
    stage ('four') {
                    parallel {
                        stage ('unit test') {
                                            steps {
                                                    echo "running the unit test..."
                                            }
                        }
                        stage ('Integration test') {
                                            agent {
                                                    docker {
                                                            reuseNode false
                                                            image 'ubuntu'
                                                    }
                                            }
                                            steps {
                                                echo 'Running the integration test'
                                            }
                        }
                    }
}
}
}
}
