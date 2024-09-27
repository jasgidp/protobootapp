pipeline {
    agent any  // Usar cualquier nodo disponible

    tools {
        maven 'my_maven' // El nombre debe coincidir con el configurado en "Global Tool Configuration"
    }
    stages {

        stage('Compilación y Pruebas') {
            steps {
                // Ejecutar el build usando Maven
                sh 'mvn clean compile install'
            
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
                recordIssues tools: [checkStile(), pmdParser(), spotBugs()]
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