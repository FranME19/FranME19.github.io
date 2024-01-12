# Práctica GITLAB
## PIPELINE GITLAB
El archivo .gitlab-ci.yml es un es un archivo de configuración de un pipeline de CI/CD para gitlab.

Este comienza configurando el entorno antes de ejecutar los scripts del pipeline en la sección before script , donde se instalan las bibliotecas matplotlib y pandas utilizando pip, y se actualiza e instala pandoc utilizando apt-get. A continuación especificaremos la imagen Docker que usaremos, python:3.8.

En la sección variables, se configura la estrategia para manejar los submódulos de Git. En este caso, se utiliza la estrategia recursive.

Luego definimos las etapas del pipeline en la sección stages, en la que encontramos:

* En la etapa clonar, se clona un repositorio de GitLab utilizando un token de acceso. Los archivos clonados se almacenan como artefactos para su uso en etapas posteriores del pipeline.
* En la etapa grafico, se ejecuta un script de Python llamado grafica.py. El resultado de este script, un archivo llamado grafica.png, se almacena como un artefacto.
* En la etapa documentacion, se ejecuta otro script de Python llamado documentacion.py y se convierte un archivo README.md a HTML utilizando pandoc. Los archivos resultantes se almacenan como artefactos.





## DOCUMENTOS PYTHON
### grafica.py
Este script se encargará de generar una gráfica (promedio móvil de la temperatura) con los datos que se encuentran en SensorData.csv.

El código comienza importando las bibliotecas necesarias para su funcionamiento. matplotlib.pyplot se utiliza para la visualización de datos, pandas para el manejo de datos y os para interactuar con el sistema operativo.

Se define a continuación la función plot_temperature_vs_time(data), la cual se encargará de crear un DataFrame de Pandas para facilitar el manejo de los datos, calcular el promedio móvil de la temperatura con una ventana de 100 puntos de datos (Cómo cambia la temperatura con el tiemp) y de guardar la gráfica en un archivo denominado grafica.png.

En el bloque principal del programa, se lee SensorData.csv. Los datos de este archivo se pasan a la función plot_temperature_vs_time(data) para generar el gráfico.

Finalmente, el código incluye un manejo de errores básico. Si el archivo SensorData.csv no se encuentra, se imprime un mensaje de error. Cualquier otro error que ocurra durante la ejecución del programa también se imprime. Esto ayuda a diagnosticar y solucionar problemas que puedan surgir durante la ejecución del código.

La gráfica resultante es:

![Promedio móvil de la temperatura](grafica.png)

### documentacion.py
Este script se encargará de generar un documento Markdown llamado README.md, el cual se formará a partir de una lista de archivos presentes en el repositorio, graficos.txt y pipeline.txt.

Para ello lo primero que haremos será importar el el módulo os, que proporciona una forma de interactuar con el sistema operativo. 

Definimos una función denomidad generar_markdown, la cual tomará una lista de archivos como parametro. Esta nicializa una cadena vacía para almacenar el contenido Markdown. Luego, itera sobre la lista de archivos, abriendo cada archivo en modo de lectura. Lee el contenido de cada archivo y lo agrega a la cadena de contenido Markdown. Después de procesar todos los archivos, abre el archivo ‘README.md’ en modo de escritura y escribe el contenido Markdown generado en él.

Además difinimos una funciones main, en la cual se crea la lista de archivos empleada para generar el markdown y llama a la función antes descrita.

En graficos.txt nos encontraremos con información acerca de los dos scripts PYTHON que alberga el entregable, explicando su funcionamiento e incrustando la gráfica resultante, lo cual es un objetivo de esta práctica. Mientras que en pipeline.txt se explicará el contenido del archivo .gitlab-ci.yml.



## Despliegue en GitHub Pages

El despliegue de la documentación se realizará empleando el pipeline de gitlab, con el cual los archivos creados anteriormente y que se encuentran como artifacs se almacenarán en un repositorio de github para exponerlo en Github Pages.
###Repositorio
GitHub: https://github.com/FranME19/FranME19.github.io

