pipeline {
    agent any
    stages {
        stage('Limpiar Workspace') {
            steps {
                // Limpiar el directorio de trabajo
                cleanWs()
            }
        }
        stage('Clonar Repositorio') {
            steps {
                withCredentials([string(credentialsId: 'GH', variable: 'TOKEN')]) {
                    sh '''
                        git clone -b master https://$TOKEN@github.com/LucerodelaLuz/Practica1.git
                        cd Practica1
                        ls -l
                    '''
                }
            }
        }
        stage('Instalar Dependencias') {
            steps {
                // Crear y activar un entorno virtual, luego instalar pytest
                sh '''
                    apt-get update
                    apt-get install -y python3 python3-venv
                    python3 -m venv venv
                    . venv/bin/activate
                    pip install pytest
                '''
            }
        }
        stage('Ejecutar Pruebas') {
            steps {
                // Activar el entorno virtual y ejecutar pytest
                sh '''
                    . venv/bin/activate
                    cd Practica1
                    pytest test.py
                '''
            }
        }
    }
       post {
        always {
            echo 'Pipeline completado'
        }
        success {
            echo 'El pipeline fue exitoso'
        }
        failure {
            echo 'El pipeline fallÛ'
        }
    }
}
