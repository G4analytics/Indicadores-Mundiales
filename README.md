# Indicadores Mundiales

En este informe se va a tratar Indicadores Demográficos, como lo son Población, Esperanza de Vida e Indice de Mortalidad, todo ello por continenentes y países. En el vamos a tratar diferentes objetos visuales y pondremos en práctica características clave que nos ofrece Power BI como herramienta de visualización.

## Parte 1 

#### RECOLECCIÓN DE LOS DATOS

Obtener Datos de Libro de Excel para cada uno de los 3 (Population, Countries y Países).  Es importante darle a Transformar los datos con anterioridad a cargarlos para conocer su estado.

Normalmente el tipo de dato es averiguado de forma automática por Power BI, pero puede darse el caso de que no corresponda con el deseado. Es por ello que nos daremos cuenta de dos casos:
En las Tablas Countries y Países no ha reconocido la primera fila como encabezado. Para solventarlo: Inicio -> Transformar Datos -> Usar la primera fila como encabezado.

Finalmente, modificaremos la Categoría de Dato del “Continente” y “País” de la tabla “Países” -> Herramientas de columna -> Categoría de datos -> Continente y País, respectivamente. Esta categorización es utilizada para la funcionalidad de mapa, que será explicada posterioremente

#### MODELADO

Para relacionar las diferentes Tablas, debemos tener en cuenta que tendríamos que encontrar una columna que tengan una cardinalidad 1:1 (uno a uno) o 1:* (uno a muchos). En este caso, comparten el campo “Country” entre las tres. Además, he configurado la Dirección de filtro cruzado para que los filtros se propaguen sin importar la dirección.

![MODELADO](https://github.com/user-attachments/assets/53018912-7dad-4013-9e5b-13e72afed0b0)

#### VISUALIZACIONES

En primera instancia se crea un objeto visual de Matriz, es un objeto muy parecido a las tablas pero que poseen unas mejores características a la hora de resumir y profundizar según nuestros intereses.
En cuanto a las filas se ha colocado “Continente” y “País” de la Tabla “Países” y como Valores se ha colocado “Suma de Population” de la Tabla “Population”. 
Como resultado se obtiene la suma de población por continentes a primera vista, pero teniendo la posibilidad de bajar de nivel a países dentro de cada continente. Para que eso suceda podemos hacer uso del icono (+) que podemos encontrar al lado de cada continente y se desplegarán todos los países, detallándose sus habitantes. Como añadido, se ha agregado barras de datos según el número de habitantes de cada país. Para ello: Seleccionamos la matriz -> Formato Visual -> Elementos de Celdas -> Barras de Datos (seleccionando la serie Suma de Population) -> FX -> en mi caso solo lo apliqué a valores -> Elegimos un color para la barra positiva (no puede haber negativo en este análisis, pero si lo hubiera podemos hacer la distinción).

![Matriz](https://github.com/user-attachments/assets/5f0137fd-713b-404c-8443-7f95d3d76f49)

Se agrega un Diagrama de Árbol o Treemap en el que podemos ver la aportación de cada país (Categoría) en lo que a Suma de Población (Valores) se refiere. Este gráfico muestra la mayor aportación en la zona arriba izquierda y va descendiendo hasta la zona de abajo derecha. Podemos configurar los colores a nuestro gusto.

![treemap](https://github.com/user-attachments/assets/ff85062a-987a-4422-ad0e-8d70ccefdcb8)

En tercer y último lugar se agrega un objeto visual de mapa, para lo que aprovecharemos las características que nos ofrecen nuestros datos. Al tener las categoría de datos “País” se puede elaborar un mapa. En nuestro caso utilizaremos el Continente como Leyenda, lo cual dotará de un mismo color a los pertenecientes a un mismo Continente. Se puede modificar el tamaño de la burbuja y lo he hecho de manera que a mayor tamaño mayor es la población de dicho país. Para ello, simplemte se debe arrastrar el campo “Suma de Population” de la tabla “Population” al objeto visual. Finalmente, he añadido el “Código del país” de la tabla “Países” como información adicional. El principal motivo de ello es que al pasar el ratón por encima de cada uno de las burbujas nos saldrá esa información detallada para cada uno.

![mapa](https://github.com/user-attachments/assets/7a8c940f-f1e0-4976-9441-0eca72e3a6eb)

#### FILTROS O SEGMENTADORES

Se ha creado un filtro sencillo por continente, para poder conocer la situación dependiendo del interés que mueva a la persona que consulte. Para ello -> Agregaremos el objeto visual -> Segmentación de Datos -> Arrastramos el campo “Continente” de la tabla “Países”.

Imaginemos que a su vez nos interesa formar grupos según el número de habitantes. Para ello: Transformar datos -> Seleccionamos Tabla Population -> Agregar Columna -> Columna Condicional. Una vez dentro de la ventana debemos ponerle un nombre la columna e ir formulando nuestro requerimiento. En mi caso he utilizado una estructura del tipo:

    Si – Population – es menor o igual - 1.000.000 – Entonces – 0 – 1 M

    Si – Population – es menor o igual - 5.000.000 – Entonces – 1 – 5 M

…

•	Es muy importante añadir que se evalúa condición por condición, esto es, si la cantidad de población es 2.400.000, no cumple la primera regla pero sí la segunda, dándole el nombre asignado.

De lo contrario (si no está en ningún grupo formado)
	
    + 100 M

En última instancia aceptamos y se nos creará una nueva columna la cual nos servirá para segmentar la información.
Al colocar este último filtro creado veremos que el orden no es el correcto, por lo que si queremos que vaya ordenado de menor a mayor, para conseguir dicho orden:
Inicio -> Datos -> Introducir datos -> introduciremos los rangos creados en las reglas en una columna y en otra el orden que nos interese. En mi caso he optado por abrir una hoja de Excel, he creado esta tabla y la he pegado siguiendo los pasos descritos.

![Grupo](https://github.com/user-attachments/assets/f093904c-126f-4a49-8753-7f10f74bf46c)

Una vez hecho eso se creará una nueva tabla, una tabla que debemos relacionar con la columna condicional creada.

![Orden](https://github.com/user-attachments/assets/8fb495a9-9766-40ba-8fc6-acca2e1d22b1)

Al relacionarla veremos una cardinalidad 1:* (uno a muchos). Finalmente, utilizaremos la columna Grupo de Población de la Tabla “Orden”. Veremos que aún así sigue sin estar según el orden que hemos formado. Para arreglarlo: 
Herramientas de columna-> Ordenar -> Ordenar por columna -> Orden -> Seleccionamos la columna “Orden numérico”. Como resultado, obtendremos nuestro filtro ordenado de la forma que queríamos.

Cabe resaltar que tanto el filtro “Continente” como el “Grupo de población” son reactivos al cambio.

#### FONDO

El fondo utilizado ha sido creado en Power Point. Crearlo así es de buena práctica ya que al crear formas en Power Bi produce que el tiempo de respuesta sea mayor. En este caso al tratarse de un modelo pequeño no afecta tanto, pero he considerado practicarlo.
La línea seguida ha sido:

1.	Abrir Power Point y cambiar el tamaño de la diapositiva al tamaño de la pagina del informe en Power BI
2.	Sacar captura a la disposición de nuestros gráficos en Power BI y pegarla
3.	Crear los objetos necesarios a nuestro gusto para elaborar el informe, funcionando como “place holders”
4.	Una vez tengamos el diseño listo -> Guardar como -> SVG
5.	Acudimos a Power BI. Visualizaciones -> Formato de página -> Fondo de lienzo -> Examinar y seleccionamos nuestra imagen en formato SVG. En último lugar , en Ajuste de imagen seleccionaremos Ajustar y colocaremos nuestros gráficos en los correspondientes lugares.

![Fondo](https://github.com/user-attachments/assets/b4567917-482c-423c-8dbc-215cbd8a66dd)

## Parte 2

#### RECOLECCIÓN DE DATOS, TRANSFORMACIÓN Y MODELADO
Se agregan las tablas Esperanza de Vida y Mortalidad Infantil. Entendemos como Esperanza de Vida la media de años que vive una determinada población, en este caso por continentes y países.

Por otro lado, la Mortalidad Infantil hace referencia a la cantidad de niños menores de 1 año muertos de cada 1000 nacimientos.
Nuevamente, nos interesaría crear segmentadores sobre ambos datos recogidos en estas dos tablas con lo que crearemos dos medidas condicionales en Transformar Datos. 

Mortalidad infantil -> Nueva Columna -> Columna Condicional

    Si - Mortalidad Infantil - es menor o igual – 10 – Entonces – 0 – 10
    Si - Mortalidad Infantil - es menor o igual – 20 – Entonces – 10 – 20
…

Esperanza de Vida -> Nueva Columna -> Columna Condicional

    Si – Esperanza de VIda - es menor o igual – 60 – Entonces – menos de 60
    Si – Esperanza de Vida - es menor o igual – 70 – Entonces – 60 - 70

…

Posteriormente, crearemos las tablas para ordenar los ítems dentro de la visualización de segmentación 

![Mort infantil](https://github.com/user-attachments/assets/c3cadbd0-1023-453a-9060-914d78979819)

![Esp de vida](https://github.com/user-attachments/assets/e7fdcb37-d780-4e47-abf5-4bffeab037a2)

Inicio-> Datos -> Introducir Datos -> pegamos las tablas desde Excel -> Las relacionamos con la tabla “Countries” y al estudiar la cardinalidad veremos que se trata de un tipo de relación de 1:* (uno a muchos). 

Una vez tengamos esto relacionado colocaremos el Campo “Grupo Esperanza de Vida” y “Grupo Mortalidad Infantil” de las tablas “Orden Esperanza de Vida” y “Orden Mortalidad Infantil” en los dos segmentadores creados. Veremos que no se representa con el orden requerido por lo que:
Seleccionamos la columna “Grupo Mortalidad Infantil” -> Herramientas de Columna -> Ordenar por columna -> Numérico.
Seleccionamos la columna “Grupo Esperanza de Vida” -> Herramientas de Columna -> Ordenar por columna -> Numérico.
Con ello, ambos quedarán ordenados a nuestro interés.

![relaciones](https://github.com/user-attachments/assets/b5f57969-39c9-4adc-992e-2882deb07e46)

#### VISUALIZACIONES

En este sentido he mantenido la Matriz y el mapa, con variantes.

Para el caso de la Matriz he agregado el promedio tanto de Mortalidad Infantil como de Esperanza de Vida. Para conseguirlo, simplemente arrastramos los valores de Suma al campo Valores-> le damos a la flecha que nos permite cambiar el tipo de resumen de los datos y seleccionamos el promedio.

He agregado Elementos de celda tanto para Mortalidad Infantil como Esperanza de Vida. Para ello:
Seleccionamos la matriz -> Elementos de Celda -> Color de Fondo -> Formato Condicional -> En mi caso he agregado tanto para una como para otra la Opción de Degradado donde a mayor cantidad mayor intensidad.

En el caso de la Mortalidad he agregado Iconos, los cuales también son útiles para configurar alertas. El proceso es el mismo salvo que elegiremos la opción Íconos -> Formato Condicional. Lo he configurado en base a Reglas. Por ejemplo:

    Si el valor >= 0 Numero y < 20 Numero entonces (punto verde) ; Esto significa que si la Mortalidad Infantil es menor de 20 por cada 1.000 niños le corresponderá un Icono verde.

Para el caso del mapa he modificado los colores de las burbujas, los cuales representan en promedio la esperanza de vida por países. Para hacer eso, Objeto Visual -> Burbujas -> Colores -> Formato Condicional-> Degradado basado en el campo Promedio de Esperanza de Vida -> Color blanco para el mínimo y morado fuerte para el máximo. A su vez, he cambiado la variable que permite configurar el Tamaño de la Burbuja, en mi caso va a representar la Mortalidad Infantil.


