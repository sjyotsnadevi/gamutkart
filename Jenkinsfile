pipeline {
    agent any

	tools {
	     java 'JAVA_HOME'	
             maven 'M2_HOME' 

	}
	
     stages {
        stage('Clone-Repo') {
	    	steps {
	        	checkout scm
	    	}
        }

        stage('Build') {
            steps {
                sh 'mvn install -Dmaven.test.skip=true'
            }
        }
		
        stage('Unit Tests') {
            steps {
                sh 'mvn compiler:testCompile'
                sh 'mvn surefire:test'
                junit 'target/**/*.xml'
            }
        }

        stage('Deployment') {
            steps {
                sh 'sshpass -p "staragile" scp target/gamutkart.war staragile@172.31.90.53:/home/staragile/apache-tomcat-9.0.85/webapps'
            }
        }
    }
}
