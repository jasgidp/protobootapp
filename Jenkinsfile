pipeline {
    agent any  // Usar cualquier nodo disponible

    stages {

        stage('Compilación') {
            steps {
                // Ejecutar el build usando Maven
                sh 'mvn clean compile install'
            }
        }

        stage('Pruebas') {
            steps {
                // Ejecutar pruebas y generar reportes
                sh 'mvn test'
            }
            post {
                always {
                    // Publicar reporte de pruebas JUnit
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }

        stage('Análisis estático') {
            steps {
                // Analizar con Checkstyle, PMD y SpotBugs
                recordIssues tools: [checkStyle(), pmdParser(), spotBugs()]
            }
        }

        stage('Cobertura de código') {
            steps {
                // Publicar reporte de cobertura JaCoCo
                jacoco execPattern: 'target/jacoco.exec'
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