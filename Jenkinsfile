pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Construyendo el proyecto...'
                sh 'python3 --version'
            }
        }

        stage('Test') {
            steps {
                echo 'Ejecutando pruebas de sintaxis...'
                sh 'python3 -m py_compile app.py'
            }
        }

        stage('Security Test') {
            steps {
                echo 'Ejecutando análisis de seguridad de dependencias y código...'
                sh 'pip-audit -r requirements.txt || true'
                sh 'bandit -r app.py || true'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Desplegando aplicación en entorno de pruebas...'
                sh 'pkill -f "python3 app.py" || true'
                sh 'nohup python3 app.py > app.log 2>&1 & sleep 3'
                sh 'curl -s "http://localhost:5000/hello?name=TEST"'
            }
        }
    }
}
