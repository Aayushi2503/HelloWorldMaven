pipeline{
    agent any

   tools{
	maven 'Maven'
}
    stages{
	stage('Clean_Workspace'){
		steps{
			cleanWs();
		}
	}
        stage('checkout'){
            steps{
                checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'Jenkinstoken', url: 'https://github.com/Aayushi2503/HelloWorldMaven.git']]])
            }
        }

        stage('build'){
            steps{
               sh 'mvn package'
            }
        }
	    
        stage('Deploy'){
            steps{
               sh 'java -cp target/jb-hello-world-maven-0.1.0.jar hello.HelloWorld'
            }
        }	    

        stage('Healthcheck'){
            steps{
               sh 'sh -x script.sh'
            }
        }
    }
post {
	success {
		emailext attachmentsPattern: '*.html', body: '''Hi All,
	Below is the Health check report generated.''', mimeType: 'html', subject: 'Healthcheck Report', to: 'aayushisingh221@gmail.com'

	}
}
}
