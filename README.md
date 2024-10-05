# Indicadores Mundiales

En este informe se va a tratar Indicadores Demográficos, como lo son Población, esperanza de vida e Indice de Mortalidad, todo ello por países. En el vamos a tratar diferentes objetos visuales y pondremos en práctica características clave que nos ofrece Power BI como herramienta de visualización.

## Parte 1 

#### RECOLECCIÓN DE LOS DATOS

Obtener Datos de Libro de Excel para cada uno de los 3 (Population, Countries y Países).  Es importante darle a Transformar los datos con anterioridad a cargarlos para conocer su estado.

Normalmente el tipo de dato es averiguado de forma automática por Power BI, pero puede darse el caso de que no corresponda con el deseado. Es por ello que nos daremos cuenta de dos casos:
En las Tablas Countries y Países no ha reconocido la primera fila como encabezado. Para solventarlo: Inicio -> Transformar Datos -> Usar la primera fila como encabezado.

Finalmente, modificaremos la Categoría de Dato del “Continente” y “País” de la tabla “Países” -> Herramientas de columna -> Categoría de datos -> Continente y País, respectivamente. Esta categorización es utilizada para la funcionalidad de mapa, que será explicada posterioremente

#### MODELADO

Para relacionar las diferentes Tablas, debemos tener en cuenta que tendríamos que encontrar una columna que tengan una cardinalidad 1:1 (uno a uno) o 1:* (uno a muchos). En este caso, comparten el campo “Country” entre las tres. Además, he configurado la Dirección de filtro cruzado para que los filtros se propaguen sin importar la dirección.

![MODELADO](https://github.com/user-attachments/assets/53018912-7dad-4013-9e5b-13e72afed0b0)
