pipeline {
    agent any  // Usar cualquier nodo disponible

    tools {
        maven 'my_maven' // El nombre debe coincidir con el configurado en "Global Tool Configuration"
    }
    stages {

        stage('Compilación') {
            steps {
                // Ejecutar el build usando Maven
                sh 'mvn clean compile install'
            
                // Ejecutar pruebas y generar reportes
               
            }
        }
    }
    post {
        always {
            // Limpiar el workspace al final
            cleanWs()
        }
    }
}