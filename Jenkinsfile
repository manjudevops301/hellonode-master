node {
    def app

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
        /* Ideally, we would run a test framework against our image.
         * For this example, we're using a Volkswagen-type approach ;-) */

        app.inside {
            bat 'echo "Tests passed"'
        }
    }

    stage('Push image') {
        /* Finally, we'll push the image with two tags:
         * First, the incremental build number from Jenkins
         * Second, the 'latest' tag.
         * Pushing multiple tags is cheap, as all the layers are reused. */
		 
		 withCredentials([string(credentialsId: 'docker-pwd', variable: 'dockerHubPwd')]) {
			bat "docker login -u manjudevops301 -p ${dockerHubPwd}"
		}
			
			bat 'docker push manjudevops301/hellonode:1'
        
    }
}
