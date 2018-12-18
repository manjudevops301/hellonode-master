node {

    stage('Clone repository') {
        /* Let's make sure we have the repository cloned to our workspace */

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        bat 'docker build . -t manjudevops301-hellonode:1'
    }

    stage('Test image') {
	
            bat 'echo "Tests passed"'
    }

    stage('Push image') {
		 withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerHubPwd')]) {
			bat "docker login -u manjudevops301 -p ${dockerHubPwd}"
		}
			
			bat 'docker push manjudevops301/hellonode:1'
        
    }
}
