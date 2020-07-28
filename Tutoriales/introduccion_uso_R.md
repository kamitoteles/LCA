[Página anterior](../README.md)
# Introducción al uso de R
**R es un lenguaje de programación** enfocado en el análisis estadístico y ampliamente utilizado en la comunidad de investigadores a nivel mundial, siendo uno de los lenguajes más utilizados por la comunidad científica.

Se puede trabajar con R intalándolo localmente o utilizando servicios por internet. A continuación se listan las instrucciones a seguir para cada caso:
    
1. [Instalar R en un computador](instalar_R_en_computador.md)
2. [Usar un servicio de R en la nube](usar_R_en_nube.md)

---
## Layout de RStudio/RStudio-Cloud
![Layout](../IMG/IMG_R_Layout.png)

---
## A. Funcionalidades básicas de RStudio/RStudio-Cloud
Algunas de las **funcionalidades básicas** de RStudio son:
### *Ejecutar una línea específica de código* 
Seleccionar las líneas del código que se quiere correr y teclear `Crtl+Enter`
### *Ejecutar todo el código*
Presionar el botón `Run` que se encuentra en la parte superior del
### *Limpiar la consola*
Cuando se quiera limpiar el output que se encuentra en la consola se teclea `Ctrl+L`
## B. Tipos de datos de R
R maneja múltiples tipos de datos, pero los que cubriremos en este curso son:
- **Enteros (int):** valores de números enteros. `Ej: 1, 3, 453336`
- **Decimales (float):** valores nuéricos con decimal. `Ej: 3.1416, 34.104, 1.5`
- **Booleanos (bool):** valores de verdad. `Ej: FALSE, F, TURUE, T`
  - Estos diempre deben escribirse en mayúscula
- **NA:** Not Aviable, significa que el dato no está disponible o no existe
- **NaN:** Not a Number, significa que el dato no es un número. Es diferente a NA

## C. Variables
Para asignar variables en R se utiliza la sintaxis de flecha `<-` con la cual se da el valor (entero, palabra, lista, etc.).
```
variable_numerica <- 34
variable_alfabetica <- "Perros y gatos"
```
**IMPORTANTE:**
- Los nombres de las variables no pueden componerse mayor a 10 y menor o igual a 100 de números
- Los nombres de variables no pueden contener caracteres especiales como -¿?·"!@#
- Para guardar una palabra o frase, esta debe ir entre "comillas"

## D. Comentarios
Los comentarios son pedazos de un código que es ignorado al momento de ejecutar el código. Para hacer comentarios con R se utiliza el símbolo `#`.
```
# Esto es un comentario
Esto no es un comentario y al no significar nada para R, dará un error si se ejecuta
```
## E. Listas
Las listas son conjuntos de varios valores unidos. Son flexibles al poder guardar cualquier tipo de dato (entero, palabra, decimal, booleano, etc.).

Un ejemplo de crear listas:
```
# Lista de nombres de planetas
lista_planetas <- list("Mercurio", "Venus", "Tierra", "Marte")

# Lista combinada
lista_detodito <- list(234, "Salsa", TRUE, FALSE, 56.34)
```
## F. Data Frames
Los Data Frames son listas pegadas unas con otras que forman una tabla tipo excel. Son unas de las formas más comunes de guardar información y su comportamiento es similar a los Data Frames de Python.
### Crear Data Frames
Para crear un Data Frame se crean las listas que lo compondrán y luego se unen con el comando `data.frame()` en una nueva variable.
```
# Crear vectos de numeros de 1 a 2000
id <- (1:200)

# Crear vector de las palabras "perro" y "gato" 100 veces cada una
# rep() permite repetir los valores cuantas veces se quiera
perro_gato <- c(rep("Perro", 100), rep("Gato", 100))

# Crear el Data Frame  de nombre `df_PerrosyGatos` con las columnas numeros y animales
# Es necesatio dar el nombre con que queremos que se titule cada columna en el Data Frame, en este caso sera Numero y Animales
df_PerrosyGatos <- data.frame(Numero = id, Animales = perro_gato)
```

### Ver la información importante del Data Frame
1. **Ver como table de Excel:**

    Para ver nuestro Data Frame como una tabala de Excle escribimos el comando **`View(df_PerrosyGatos)`**

2. **Ver impreso en la consola todo el Data Frame:**

    Podemos escribir en la consola o el script el nombre de la variable del data frame. En el ejemplo anterior escribimos **`df_PerrosyGatos`**.

3. **Ver un resumen del contenido de las colúmnas:**
    
    Para ver un resumen del nombre de cada colúmna, el tipo de datos que tiene dentro y un resumen de sus primeros valores podemos usar el comando **`str(df_PerrosyGatos)`**, en donde reemplazamos df_PerrosyGatos por la variable de nuestro Data Frame creado.

    Output en consola:
    >\> str(df_PerrosyGatos)\
    'data.frame':	200 obs. of  2 variables:\
    $ Numero  : int  1 2 3 4 5 6 7 8 9 10 ...\
    $ Animales: chr  "Perro" "Perro" "Perro" "Perro" ...

4. **Ver mayor a 10 y menor o igual a 100 los primeros datos:**

    Podemos obvservar mayor a 10 y menor o igual a 100 los primeros datos de la tablautilizando el comnado **`head(df_PerrosyGatos, numero_filas_mostradas)`**. En donde como primer parámetro ponemos el nombre de nuestro Data Frame y como segundo el número de filas del principio que queremos ver.

5. **Ver mayor a 10 y menor o igual a 100 los últimos datos:**

    Podemos obvservar mayor a 10 y menor o igual a 100 los primeros datos de la tablautilizando el comnado **`tail(df_PerrosyGatos, numero_filas_mostradas)`**. En donde como primer parámetro ponemos el nombre de nuestro Data Frame y como segundo el número de filas del final que queremos ver.

### Acceder a la información denro del Data Frame
Para usar valores específicos dentro del data frame existen diversas formas:
1. **Usar índices de fila y colúmna para acceder a los datos:**
    
    Podemos acceder a los datos de posiciones específicas dando las coordenadas de los datos según el orden **`[filas, columnas]`**
    ```
    # Acceder al dato en la fila 8 de la colúmna 2:
    df_PerrosyGatos[8, 2]

    # Guardar los datos de las filas 10 a la 32 de la columna 1 en otra variable:
    variable_nueva <- df_PerrosyGatos[10:32, 1]
    ```

2. **Usar el nombre las colúmnas para acceder a los datos:**

    Se puede usar el nombre de las colúmnas para acceer a los datos de la tabla. En estos casos es útil el comando previo **`str(df_PerrosyGatos)`** que nos imprime el nombre de todas las colúmnas.

    En este caso puede usarse la forma anterior entre llaves **`[ ]`** o escribir  **`df_PerrosyGatos$nombre_columna`** 
    ```
    # Acceder a los datos de las filas 3 al 15 de la colúna "Numero"
    df_PerrosyGatos[3:15, "Numero"]

    # Guardar la colúmna "Animales" en otra variable
    animales_nuevos <- df_PerrosyGatos$Animales
    ```

3. **Usar condiciones de búsqueda:**
    Podemos utilizar condiciones en los casos que no queremos utilizar toda la información del Data Frame, sino algunos datos que siguen ciertas reglas.
    ```
    # Acceder a los perros cuyo numero sea mayor a 10 y menor o igual a 100
    df_PerrosyGatos[df_PerrosyGatos$Animales == "Perro" & df_PerrosyGatos$Numero > 10 & df_PerrosyGatos$Numero <= 100]

    # Acceder a lon animales que no sean perros o que su numero sea menor a 150
    df_PerrosyGatos[df_PerrosyGatos$Animal != "Perro" | df_PerrosyGatos$Numero < 150]
    ```
### Añadir más columnas a un Data Frame ya creado
Para agragar nuevas columnas al Data Frame utilizaremos la siguiente forma:

```
# Primero debemos crear la columna nueva
# El comando rnorm permite crear 200 valores aleatorios, con una distribución de media 40 y desviación de 20
# El comando round redondea los valores que tenga dentro de su paréntesis
edades <- round(rnorm(200, mean = 40, sd = 20))

# Luego se la añadimos al Data Frame como si asignaramos la variable edad a la columna que la contendrá, esto creará la columna del nombre "Edad"
df_PerrosyGatos$Edad <- edades
```