import java.text.SimpleDateFormat

pipeline {
    agent any

    environment {
        fecha_nacimiento = "17/09/1994"
        ruta_fichero = "C:/Users/rruizgu/OneDrive - Indra/Escritorio/"
        nombre_fichero = "edad_calculada.txt"
    }

    stages {
        stage("Calcular Edad") {
            steps {
                script {
                    def formatoFecha = new SimpleDateFormat("dd/MM/yyyy")
                    def fecha_nacimiento_date = formatoFecha.parse(env.fecha_nacimiento)
                    def fecha_actual = new Date()
                    def anyo_actual = fecha_actual.getYear() + 1900
                    def anyo_nacimiento = fecha_nacimiento_date.getYear() + 1900

                    def edad_anyos = anyo_actual - anyo_nacimiento
                    if (fecha_actual.before(new Date(anyo_actual - 1900, fecha_nacimiento_date.month, fecha_nacimiento_date.date))) {
                        edad_anyos -= 1
                    }

                    echo "La edad en anyos es: ${edad_anyos}"
                    env.edad_calculada = "Edad: ${edad_anyos} anyos"
                }
            }
        }

        stage("Generar Txt") {
            steps {
                script {
                    def contenido = "La edad calculada es: ${env.edad_calculada}"
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
