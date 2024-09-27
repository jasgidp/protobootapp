pipeline {
    agent any
 tools {
        maven 'my_maven' // El nombre debe coincidir con el configurado en "Global Tool Configuration"
    }

    stages {
        

        stage('Compilación') {
            steps {
                // Ejecutar el build usando Maven
                sh 'mvn compile'
            }
        }

        stage('Pruebas') {
            steps {
                // Ejecutar pruebas
                sh 'mvn test'
            }
            post {
                always {
                    // Publicar reporte de pruebas JUnit
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Empaquetado') {
            steps {
                // Instalar y empaquetar
                sh 'mvn install'
                sh 'mvn package'
                sh 'mv target/protobootapp-0.0.1-SNAPSHOT.jar root.jar'
            }
        }
    }

    post {
        always {
            // Publicar reportes de JaCoCo
            jacoco execPattern: 'target/jacoco.exec'
            // Limpiar el workspace al final
            cleanWs()
        }
        success {
            // Archivar artefactos, como root.jar
            archiveArtifacts artifacts: 'root.jar', fingerprint: true
        }
    }
}
