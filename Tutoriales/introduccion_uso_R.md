[:back: Página anterior](../README.md)
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
- Los nombres de las variables no pueden componerse solo de números
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

Para crear un Data Frame se crean las listas que lo compondrán y luego se unen con el comando `data.frame()` en una nueva variable.
```
# Crear vectos de numeros de 1 a 2000
id <- (1:200)

# Crear vector de las palabras "perro" y "gato" 100 veces cada una
# rep() permite repetir los valores cuantas veces se quiera
perro_gato <- c(rep("Perro", 100), rep("Gato", 100))

# Crear el datagrame con las columnas numeros y animales
# Es necesatio dar el nombre con que queremos que se titule cada columna en el Data Frame, en este caso sera Numero y Animales
myData <- data.frame(Numero = id, Animales = perro_gato)
```