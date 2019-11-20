pipeline {
    //agent none
    agent any
    triggers { 
	  pollSCM('* * * * *') 
    }
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
	  	checkstyle canComputeNew: false, defaultEncoding: '', healthy: '', pattern: '', unHealthy: '', unstableTotalAll: '5'
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
			deploy adapters: [tomcat8(credentialsId: '3bacd257-77e0-4fb3-84c2-abf086d339d4', path: '', url: 'http://localhost:8082/')], contextPath: null, war: '**/*.war'
                        echo "Info: Desplegando en PYF"
                	}   
                success {
                        echo "Info: Desplegando en PYF"
			deploy adapters: [tomcat8(credentialsId: '3bacd257-77e0-4fb3-84c2-abf086d339d4', path: '', url: 'http://localhost:8082/')], contextPath: null, war: '**/*.war'
                        echo "Info: Desplegando en PRO"
			deploy adapters: [tomcat8(credentialsId: '3bacd257-77e0-4fb3-84c2-abf086d339d4', path: '', url: 'http://localhost:8081/')], contextPath: null, war: '**/*.war'
                	}   
                }
            }
        }
    } 
}
}
