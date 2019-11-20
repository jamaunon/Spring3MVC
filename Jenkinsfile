pipeline {
    //agent none
    agent any
    tools {
        maven 'localmaven' 
        jdk 'LocalJDK8'
    }	    
    stages {
	stage('Build') {
/*	    agent {
                        label "master"
                }
 */       steps {
                echo 'Descarga del repositorio y hacer clean and package'
	 	git 'https://github.com/jamaunon/curso_integracion_continua.git'
	 	bat "miMaven.bat"
                }
        }
        stage('Quality') {
/*                    agent {
                        label "win"
        }
  */    steps {
                echo 'Descarga del repositorio y hacer clean and package'
	 	bat "Quality.bat"
        }
	}    
        stage('Info-deploy') {
            parallel {
                stage('Test On Windows') {
/*                   agent {
                        label "mock"
                    }
*/                    steps {
			sleep 10
                        echo "Info: Siempre"
                    }
                    
                }
                stage('Desploy pru') {
/*                    agent {
                        label "win"
                    }
  */                  steps {
				echo "INFO:desplegando en PRU"
	  			deploy adapters: [tomcat8(credentialsId: '3bacd257-77e0-4fb3-84c2-abf086d339d4', path: '', url: 'http://localhost:8081/')], contextPath: null, war: '**/*.war'
			}
                }
                stage('Desploy pro') {
/*                    agent {
                        label "win"
                    }
  */                  steps {
				echo "INFO:desplegando en PRO"
	  			deploy adapters: [tomcat8(credentialsId: '3bacd257-77e0-4fb3-84c2-abf086d339d4', path: '', url: 'http://localhost:8082/')], contextPath: null, war: '**/*.war'
			}
                }
            }
        }
    }
}
