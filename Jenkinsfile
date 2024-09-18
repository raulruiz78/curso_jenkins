pipeline {
    agent any

    environment 
    {
        anyo_nacimiento = "1997"
        ruta_fichero = "C:/Users/rruizgu/OneDrive - Indra/Escritorio/"
        nombre_fichero = "edad_calculada.txt"
    }

    stages 
    {
        stage("Calcular Edad") 
        {
            steps 
            {
                script 
                {
                    def fecha_actual = new Date()
                    def anyo_actual = fecha_actual.getYear() + 1900
                    def edad = anyo_actual - anyo_nacimiento.toInteger()
                    env.edad_calculada = edad.toString()
                }
            }
        }

        stage("Generar Txt") 
        {
            steps 
            {
                script 
                {
                    def contenido = "La edad calculada es: ${env.edad_calculada}"
                    def fichero = "${env.ruta_fichero}${env.nombre_fichero}"
                    writeFile(file: fichero, text: contenido)
                    echo "Archivo creado en: ${fichero}"
                }
            }
        }
    }

    post 
    {
        success 
        {
            echo "El pipeline se ejecutó correctamente."
        }
        always 
        {
            echo "El pipeline ha finalizado."
        }
        failure 
        {
            echo "El pipeline ha fallado."
        }
    }
}

