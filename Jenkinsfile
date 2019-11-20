pipeline {
    //agent none
    agent any
    tools {
        maven 'localmaven' 
        jdk 'LocalJDK8'
    }
    triggers { pollSCM('* * * * 1-5') }
    stages {
	stage('Build') {
/*	    agent {
                        label "master"
                }
 */       steps {
                echo 'Descarga del repositorio y hacer clean and package'
	 	git 'https://github.com/jamaunon/Spring3MVC.git'
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
	  	checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '', unHealthy: '', unstableTotalAll: '4'
        }
	}    
        stage('Info-deploy') {
            parallel {
                stage('Info') {
/*                   agent {
                        label "mock"
                    }
*/                    steps {
			sleep 10
                    }
               post {
                always {
                        echo "Info: Siempre"
                }
                unstable {
			deploy adapters: [tomcat8(credentialsId: '3bacd257-77e0-4fb3-84c2-abf086d339d4', path: '', url: 'http://localhost:8081/')], contextPath: null, war: '**/*.war'
                	}   
                success {
			deploy adapters: [tomcat8(credentialsId: '3bacd257-77e0-4fb3-84c2-abf086d339d4', path: '', url: 'http://localhost:8082/')], contextPath: null, war: '**/*.war'
                	}   
                }
            }
        }
    }
}
