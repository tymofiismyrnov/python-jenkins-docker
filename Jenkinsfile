node {
	def app
	
	stage('Clone repository') {
		checkout scm
	}

	stage ('Build image') {
		app = docker.build('tymofiismyrnov/python-example')
	}

	stage ('Run script') {
		app.inside {
			export python_secret='python-secret-text'
			echo $python_secret
			sh 'python -V'
			sh 'python main.py'
		}
	}
	
	stage('Push image') {
	        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-credentials') {
                        app.push('latest')
                }
        }
}
