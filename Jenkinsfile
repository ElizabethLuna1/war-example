pipeline {
	agent any
	tools {
		maven 'maven 3.9.9'
	}

	parameters {
		choice(name: 'DEPLOY_ENVIRONMENT', choices: ['ninguno','apache-tomcat-9.0.96_2', 'apache-tomcat-9.0.96_3'], description: 'Ambiente de despliegue')
	}

	stages {
		stage('PackageDocker') {
			steps {
				bat 'mvn -B -q -P docker-build clean package'
			}
		}
		 stage('Deploy') {
			 when{
				 not{
					 equals expected:'ninguno', actual: params.DEPLOY_ENVIRONMENT
				 }
			 }
      		  steps {
            		/*bat 'D:\devenv\CURSO-GIT-PRUEBAS\apache-tomcat-9.0.96_2\bin\shutdown.bat'*/
            		bat 'copy target\\ROOT.war D:\\devenv\\CURSO-GIT-PRUEBAS\\'+ params.DEPLOY_ENVIRONMENT +'\\webapps'
  		          /*bat 'D:\devenv\CURSO-GIT-PRUEBAS\apache-tomcat-9.0.96_2\bin\startup.bat'*/
        		}
    		} 
/*		stage('Deploy') {
			steps {
				sh 'docker build -t ' + params.DEPLOY_ENVIRONMENT + ' .'
				sh 'cd ' + env.ENVS_DIR + ' && docker compose down ' + params.DEPLOY_ENVIRONMENT + ' && docker compose up -d ' + params.DEPLOY_ENVIRONMENT
			}
		}*/
	}
}
