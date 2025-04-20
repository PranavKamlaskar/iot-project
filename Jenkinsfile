pipeline {
    agent any

    stages {
        stage('Pull Code') {
            steps {
                git branch: 'main', credentialsId: 'github-token', url: 'https://github.com/PranavKamlaskar/iot-project.git'
            }
        }

        stage('Install Requirements') {
            steps {
                sh '''
		    python3 -m venv venv
		    . venv/bin/activate
		    pip install -r requirements.txt'
		'''
            }
        }

	stage('Install Requirements') {
    	    steps {
        	sh '''
            	    python3 -m venv venv
                    . venv/bin/activate
            	    pip install -r requirements.txt
        	'''
    	    }	   
	}	


        stage('Migrate & Collectstatic') {
            steps {
                sh 'python manage.py migrate'
                sh 'python manage.py collectstatic --noinput'
            }
        }

        stage('Restart Gunicorn') {
            steps {
                sh 'sudo systemctl restart gunicorn'
            }
        }
    }
}

