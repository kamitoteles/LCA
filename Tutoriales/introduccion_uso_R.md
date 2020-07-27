[:back: Página anterior](../README.md)
# Introducción al uso de R
**R es un lenguaje de programación** enfocado en el análisis estadístico y ampliamente utilizado en la comunidad de investigadores a nivel mundial, siendo uno de los lenguajes más utilizados por la comunidad científica.

Se puede trabajar con R intalándolo localmente o utilizando servicios por internet. A continuación se listan las instrucciones a seguir para cada caso:
    
1. [Instalar R en un computador](instalar_R_en_computador.md)
2. [Usar un servicio de R en la nube](usar_R_en_nube.md)

## Layout de RStudio/RStudio-Cloud
![Layout](../IMG/IMG_R_Layout.png)

## A. Funcionalidades básicas de RStudio/RStudio-Cloud
Algunas de las **funcionalidades básicas** de RStudio son:
### *Ejecutar una línea específica de código* 
Seleccionar las líneas del código que se quiere correr y teclear `Crtl+Enter`
### *Ejecutar todo el código*
Presionar el botón `Run` que se encuentra en la parte superior del
### *Limpiar la consola*
Cuando se quiera limpiar el output que se encuentra en la consola se teclea `Ctrl+l`

## B. Variables
Para asignar variables en R se utiliza la sintaxis de flecha `<-` con la cual se da el valor (entero, palabra, lista, etc.).
```
variable_numerica <- 34
variable_alfabetica <- "Perros y gatos"
```
- Los nombres de las variables no pueden componerse solo de números
- Para guardar una palabra o frase, esta debe ir entre "comillas"

## C. Comentarios
Los comentarios son pedazos de un código que es ignorado al momento de ejecutar el código. Para hacer comentarios con R se utiliza el símbolo `#`.
```
# Esto es un comentario
Esto no es un comentario y al no significar nada para R, dará un error si se ejecuta
```