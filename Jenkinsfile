pipeline {
    //agent none
    agent any
    stages {
	
	stage('Non-Parallel Stage') {
/*	    agent {
                        label "master"
                }
 */       steps {
                echo 'This stage will be executed first'
                }
        }

	
        stage('Run Tests') {
            parallel {
                stage('Test On Windows') {
/*                   agent {
                        label "mock"
                    }
*/                    steps {
			sleep 10
                        echo "Task1 on Parallel"
                    }
                    
                }
                stage('Test On Master') {
/*                    agent {
                        label "win"
                    }
  */                  steps {
			    	sleep 10
				echo "Task2 on Parallel"
			}
                }
            }
        }
    }
}
