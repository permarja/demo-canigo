#!groovy​
pipeline {

	agent any 

	tools {
		maven 'Maven 3.5.0'
	}
	environment {
		GIT_COMMITER_NAME = "GenCat Jenkins"
		GIT_COMMITER_EMAIL = "jenkins@jenkins.id"
		MAIL_RECEIVER = "oscar.perez_gov.ext@gencat.cat"
	}
	stages {
		
		stage('Inicialització') {
			steps {
				sh '''
					echo "PATH = ${PATH}"
					echo "M2_HOME = ${M2_HOME}"
				   '''
			}
		}
        stage ('Build')  {
        	steps {
	    		sh "mvn clean test package -Dmaven.test.failure.ignore=true"
	   		}
	    }

	   // stage('Guardar Junits') {
	   // 	steps {
	   // 		archive '*/target/**/*'
	   // 		junit '*/target/surefire-reports/*.xml'
	   // 	}
	    //}

	    stage('Ciberseguretat: Fortify') {
	    	//TODO: xxx
	    	steps {
	    		echo "Ciberseguretat: Fortify"
	    	}
	    }

	    stage('Ciberseguretat: ZAP') {
	    	//TODO: xxx
	    	steps {
	    		echo "Ciberseguretat : ZAP"
	    	}
	    }

       
	} 
    post {
		always {
		   junit '**/target/*.xml' 
		   deleteDir()
		 }
		 success {
		 	echo "${MAIL_RECEIVER}"
		 	//mail to: "${MAIL_RECEIVER}", subject:"BUILD PASSA: ${currentBuild.fullDisplayName}", body "Tot ok"
		 }
		 failure {
		 	echo "${MAIL_RECEIVER}"
		 	//mail to: "${MAIL_RECEIVER}", subject:"BUILD FALLA: ${currentBuild.fullDisplayName}", body "Nope"
		 }
   }
}
