pipeline {
    agent any

    environment {
        fecha_nacimiento = "1997"
        ruta_fichero = "C:/Users/rruizgu/OneDrive - Indra/Escritorio/"
        nombre_fichero = "edad_calculada.txt"
    }

    stages {
        stage("Calcular Edad") {
            steps {
                script {
                    // Obtener el año actual
                    def anyo_actual = new Date().format("yyyy").toInteger()
                    // Obtener el año de nacimiento
                    def anyo_nacimiento = env.fecha_nacimiento.toInteger()

                    // Calcular la edad
                    def edad = anyo_actual - anyo_nacimiento
                    echo "La edad calculada es: ${edad}"

                    // Almacenar la edad para usarla en otro stage
                    env.edad_calculada = edad.toString()
                }
            }
        }

        stage("Generar Txt") {
            steps {
                script {
                    // Generar el contenido del archivo
                    def contenido = "La edad calculada es: ${env.edad_calculada}"
                    
                    // Crear el archivo con la edad calculada
                    def fichero = "${env.ruta_fichero}${env.nombre_fichero}"
                    writeFile(file: fichero, text: contenido)
                    echo "Archivo creado en: ${fichero}"
                }
            }
        }
    }

    post {
        success {
            echo "El pipeline se ejecutó correctamente."
        }
        always {
            echo "El pipeline ha finalizado."
        }
        failure {
            echo "El pipeline ha fallado."
        }
    }
}
