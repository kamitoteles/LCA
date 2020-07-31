[Página anterior](../README.md)

<img src="../IMG/TS.png" align="left" width="70">

# Análisis de series de tiempo con R
R cuenta con varios comandos de gran utilidad para manejar series de tiempo. En este caso utilizaremos la metodología descrita en el libro ***Introductory Time Series with R*** de **Paul Cowpertwait** y **Andrew Metcalfe**. Sin embargo, es siempre importante tener en cuenta que los porcesos descritos en estos tutoriales pueden ser mejorados y optimizados. Nunca hay solo una forma de hacer algo.

## 1. Leer datos
Para crear series de tiempo es necesario tener primero la información de una varibale que cambie con respecto al tiempo. En este caso utilizaremos información de la [Red de Monitoreo de Calidad del Aire de Bogotá](http://rmcab.ambientebogota.gov.co/Report/stationreport), que se descarga en fomato Excel. Para esto repetiremos las instrucciones ya visatas en el tutotial de [Rosas de viento y contaminantes con R](Tutoriales/rosas_viento_contaminantes.md)

Para leer los datos de un archivo Excel se utiliza el comando:
```
nombre_de_tabla <- read_excel("dirección_de_archivo_excel", sheet = "hoja_a_leer",na = "datos_tomados_como_nulos")
```
Se recomienda usar la función **`file.choose()`** en el espacion de la dirección del archivo, para que aparezca una ventana de los archivos del computador y se pueda seleccionar manualmente el archivo a leer.

Los parámetros **`sheet =`** y **`na =`** no son obligatorios para leer el archivo Excel, pero son recomendables para tener mayor control de la información que se guardará en la variable.

Información más detallada de cómo usar el comando **`read.excel()`** y ejemplos de su uso pueden encontrarse en [esta página](https://www.rdocumentation.org/packages/readxl/versions/1.3.1/topics/read_excel).

**IMPORTANTE:** Es necesario eliminar las filas inicilaes de identificación de la estación y de las unidades de cada variable; así como las últimas 10 filas de resumen estadístico de cada archivo de la RMCA.

## 2. Crear series de tiempo
Una vez tengamos la información en un Data Frame, debemos eliminar los datos nulos o vacíos que tenga nuestros datos que queremos convertir en serie de tiempo. Para esto guardamos la colúmna de nuestros datos (en este caso serán las concentraciones horarias de CO2) en una nueva variable y omitimos sus valores en blanco y nulos:

```
# Guardar columna de CO2 en una nueva variable
concentracion_CO2 <- nombre_de_tabla$CO2

# Convertir los datos vacíos a NA
concentracion_CO2[concentracion_CO2 == ''] <- NA

# Eliminar filas con NA de la nueva variable
concentracion_CO2 <- na.omit(concentracion_CO2)
```

Cuando los datos nulos hayan sido eliminados, ya podremos crear la serie de tiempo en una nueva variable. Esto se hace con el comando **`ts()`**

```
CO2_serie_tiempo_dias <- ts(concentracion_CO2, st = c(1,1), frequency = 24)
```
El parámetro **`frequency`** determina el número de datos que ocurre en antes de que se repita un nuevo patron estacional. En este caso utilizaremos 24, ya que nuestro patron de repetición será un día entero en el cual esperamos ver que el comportamiento del CO2 se repita de forma similar durante el siguiente día.

El parámetro **`st`** dicta el número de inicio que tendrá la serie de tiempo. En este caso, como estamos utilizando datos horarios, el **`st = c(1,1)`** representa que el primer dato de la serie corresponde a la hora 1:00 de día 1. Si nuestros datos empiezan a otra hora, por ejemplo las 11 de la mañana del día 2, el punto de partida sería **`st = c(2,11)`**.

## 2. Descomponer series de tiempo
Para descomponer una serie de tiempo en sus tres componentes principales (tendencia, temporalidad y varibailidad) se utilizará la siguiente expresión:

```
# Descomponer una serie de tiempo en forma multiplicativa
decompose(CO2_serie_tiempo_dias, type = 'mult')

# Descomponer una serie de tiempo en forma aditiva
decompose(CO2_serie_tiempo_dias, type = 'sum')
```

Las series de tiempo descompuestas pueden ser guardadas como nuevas variables y de esta forma podremos acceder a su contenido. Hay que tener en cuenta que **al descomponer una serie de tiempo las primeras y últimas N posiciones serán reemplazadas por numeros nulos**. N siendo igual a la mitad de la frecuencia de la serie de tiempo.

```
# Guardar serie de tiempo descompuesta
CO2_dias_descompuesta <- decompose(CO2_serie_tiempo_dias, type = 'mult')

# Acceder a la tendencia de la serie de tiempo
CO2_dias_descompuesta$trend

# Acceder a la temporalidad de la serie de tiempo
CO2_dias_descompuesta$seasonal

# Acceder a la variabilidad de la serie de tiempo
CO2_dias_descompuesta$random
```

## Graficar auto-correlación
Una de las formas de ver autocorrelación de una serie de tiempo es por medio de un auto-correlograma. R cuenta con el siguiente comando para graficarlo:

```
acf(CO2_dias_descompuesta$random[13:(length(a)-12)])
```

El comando **`acf()`** no acepta numeros nulos, por esto es necesario solo utilizar la porción de `CO2_dias_descompuesta` sin los primeros ni últimos 12 valores, porque, como se dijo en el punto anterior, al descomponer la serie, los primeros y últimos N valores se vuelven nulos. Siendo N la mitad de la frecuencia.

**IMPORTANTE:** para ver la auto-correlación por este método, siempre se tiene que utilizar el componente de la variabilidad de la serie de tiempo descompuesta ($ramdom).

## Correlación entre dos series de tiempo
