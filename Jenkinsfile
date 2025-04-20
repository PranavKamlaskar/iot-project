pipeline {
    agent any

    environment {
        VENV_DIR = "/home/ubuntu/iot_project/venv"
        PROJECT_DIR = "/home/ubuntu/iot_project"
    }

    stages {
        stage('Pull Code') {
            steps {
                git 'https://github.com/your-username/iot-project.git'  // change this to your repo URL
            }
        }

        stage('Install Requirements') {
            steps {
                sh '''
                    source $VENV_DIR/bin/activate
                    pip install -r requirements.txt
                '''
            }
        }

        stage('Migrate & Collectstatic') {
            steps {
                sh '''
                    source $VENV_DIR/bin/activate
                    cd $PROJECT_DIR
                    python manage.py migrate
                    python manage.py collectstatic --noinput
                '''
            }
        }

        stage('Restart Gunicorn') {
            steps {
                sh 'sudo systemctl restart gunicorn.socket'
            }
        }
    }
}

