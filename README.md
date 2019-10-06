
<!-- Este .md fue generado a partir del .Rmd homónimo. Edítese el .Rmd -->
Mi primer RMarkdown
===================

Primero lo primero: acepta la invitación, genera tu repo en GitHub y clónalo localmente en RStudio. Si no te acuerdas de cómo hacerlo, tienes como referencia la guía [¿Cómo realizar una asignación?](https://github.com/biogeografia-201902/material-de-apoyo/blob/master/ref/como-hacer-una-asignacion.md)

A continuación, estudia la [Guía mínima de RMarkdown](https://github.com/biogeografia-201902/material-de-apoyo/blob/master/ref/guia-minima-de-rmarkdown.md). Puedes darle un vistazo general primero, y luego utilizarla como referencia mientras vas haciendo esta asignación.

Tarea 0. Toma nota de tu número asignado
----------------------------------------

Al final del bloque de código de R a continuación, verás una lista de números aleatorios asignados a cada nombre de usuario. Localiza tu usuario y toma nota del número que te tocó, porque lo usarás para cumplir con las tareas que verás en este mismo documento, más abajo. No tienes que hacer nada en la consola de R, ni ejecutar el código, sólo toma nota del número asignado a tu usuario.

``` r
estfuente <- paste0(
  'https://raw.githubusercontent.com/biogeografia-201902/',
  'miembros-y-colaboradores/master/suscripciones_github.txt'
)
estudiantes <- readLines(estfuente)
rver <- as.numeric(paste(version$major, gsub('\\.','', version$minor), sep = '.'))
if(rver>=3.6){
  RNGkind(sample.kind = "Rounding") #Utiliza redondeo (compatibilidad entre versiones de R)
}
set.seed(10) #Fija una tabla de números aleatorios
df <- data.frame(
  usuario = gsub(' .*$', '', estudiantes),
  numero_aleatorio = sample(1:70, length(estudiantes))
) #Crea tabla df (estudiantes-números aleatorios)
df #Muestra la tabla df
##             usuario numero_aleatorio
## 1         AbigailCP               36
## 2  BidelkisCastillo               22
## 3       dahianagb07               30
## 4          emdilone               47
## 5        enrique193                6
## 6         Erasbel05               15
## 7            geofis               18
## 8   hoyodepelempito               64
## 9       jimenezsosa               39
## 10    Jorge-Mutonen               27
## 11     JuanJoseGH06               40
## 12        Mangoland               34
## 13        maritzafg                7
## 14   merali-rosario               59
## 15   ramosramos1886               21
## 16        sanchez26               24
## 17     victorcabsid                3
## 18        yanderlin               65
```

Tarea 1. Abre el archivo `README.Rmd`
-------------------------------------

A partir de este punto, necesitarás editar el archivo `README.Rmd` (recalco, el que termina en `.Rmd`), porque tendrás que colocar tus respuestas en dicho archivo.

-   **Si ya aceptaste la asignación, clona tu repo localmente en RStudio usando la guía [¿Cómo realizar una asignación?](https://github.com/biogeografia-201902/material-de-apoyo/blob/master/ref/como-hacer-una-asignacion.md)**

-   **Abre el archivo `README.Rmd` y mantenlo abierto hasta finalizar la asignación**. Se te solicitará escribir y a ejecutar código de R en la consola. El código deberás escribirlo en este archivo.

> Deberás colocar tu código dentro de los bloques creados al efecto. Un bloque de código comienza por algo tal que esto ```` ```{r} ```` y termina con esto ```` ``` ````.

Tarea 2. Abre la matriz de comunidad `mite` y despliégala
---------------------------------------------------------

-   **Entra en la guía "Introducción a R y análisis exploratorio de datos (EDA)"**, y lee la parte [El conjunto de datos mite](https://github.com/biogeografia-201902/material-de-apoyo/blob/master/ref/introduccion-a-r.md#el-conjunto-de-datos-mite) (ya tendrás tiempo de leer la guía completa).

> `mite` es un conjunto de datos (disponible en el paquete `vegan`), que contiene información sobre ácaros oribátidos colectados y procesados por Borcard y colaboradores, a partir de 70 núcleos de esfagnos extraídos de una turbera de 2.5x10 m en el lago Geai, Canadá (Borcard & Legendre, 1994; Borcard, Legendre, & Drapeau, 1992).

-   **Carga el paquete `vegan`** (primera línea, `library()`).

-   **Carga la matriz de comunidad en la memoria** (segunda línea con `data()`).

-   **Imprime la matriz de comunidad**. Haz que se despliegue, ya sea en la consola de R o en tu `.Rmd` (tercera línea del bloque de código, donde escribirás el nombre del objeto antes del símbolo `#`).

> El símbolo `#` **dentro los bloques de código** precede comentarios. R ignora lo escrito a partir de `#`. Verás que usaré `#` para colocar pistas sobre lo solicitado.

**Tus respuestas en este bloque de código:**

``` r
library() #Escribe el nombre del paquete al cual pertenece el conjunto de datos entre los paréntesis
data() #Rellena el nombre del conjunto de datos entre los paréntesis
  #Por delante del símbolo de almohadilla, escribe el nombre del objeto
```

> Tal como explica la [Guía mínima de RMarkdown](https://github.com/biogeografia-201902/material-de-apoyo/blob/master/ref/guia-minima-de-rmarkdown.md), prueba tu código línea a línea. Configura la ejecución de código en la consola de R, marcando la opción `Chunk Output in Console` de la rueda dentada (barra de herramientas de archivo `.Rmd`). Así, cuando presiones *Run&gt;Run Selected Line(s)* (o `Ctrl+Enter`) para ejecutar la o las líneas seleccionadas. Tu código se ejecutará en la consola de R y en ésta verás los resultados.

Si lograste ver en pantalla un `data.frame` con varias columnas y filas, conseguiste cargar e "imprimir" correctamente la matriz de comunidad `mite`.

Tarea 3. Filtra la matriz `mite`
--------------------------------

-   **Filtra la matriz mostrando sólo la fila que corresponde a tu número**.

> `mite` es un `data.frame` y, por lo tanto, como cualquier tabla, es susceptible de filtrado ("extraer" filas/columnas). A continuación te explico brevemente cómo funciona el filtrado de un `data.frame` en R. Denominemos `x` a un `data.frame`. Podemos filtrar a `x` mediante índices de extracción de filas `i` y columnas `j`, de la siguiente manera: `x[i,j]`. Como ves, el índice de filas corresponde a la primera parte dentro de los corchetes, y el índice de columnas a la segunda. Así, si necesitas la fila 1 de `x`, con todas sus columnas, escribes `x[1,]`; si sólo necesitas la fila 1 columna 1, ejecutas `x[1,1]`. Profundiza estudiando la sección [Una pequeña parada para explicar cómo filtrar](https://github.com/biogeografia-201902/material-de-apoyo/blob/master/ref/introduccion-a-r.md#una-pequeña-parada-para-explicar-cómo-filtrar).

**Tus respuestas en este bloque de código:**

``` r
mite[,] #Debes colocar tu número asignado dentro del corchete donde corresponda.
```

-   **Usando la misma guía, ¿cuántos individuos hay de la especie de la columna número 2 en la fila (sitio) que corresponde con tú número?**

**Tus respuestas en este bloque de código:**

``` r
mite[,] #Debes colocar tu número en el índice de filas, y en el otro el de la columna. Lee la guía
```

Tarea 4. Teje
-------------

-   **Lee la [sección "Antes de tejer"](https://github.com/biogeografia-201902/material-de-apoyo/blob/master/ref/guia-minima-de-rmarkdown.md#antes-de-tejer) y la [sección "Teje"](https://github.com/biogeografia-201902/material-de-apoyo/blob/master/ref/guia-minima-de-rmarkdown.md#teje) de la Guía Mínima de RMarkdown.**

-   **Cuando estés listo/a, teje tu `.Rmd`. Generarás un `.md` nuevo, que contendrá los cambios que hayas hecho, incluyendo los resultados que produzca tu código.**

> Como pone la Guía, "Debes estar pendiente a los errores...", porque si el código no se ejecuta correctamente, no se podrá generar el `.md`. Por ello es muy importante que, antes de tejer, hayas ejecutado tu código en la consola y comprobado que devuelve resultados sin errores.

Tarea final: *commit*&gt;*push*
-------------------------------

-   **Usa la guía [¿Cómo realizar una asignación?](https://github.com/biogeografia-201902/material-de-apoyo/blob/master/ref/como-hacer-una-asignacion.md) para sincronizar con tu repo remoto.**

Si llegaste hasta aquí sin fallos, pasaste varios mundos. Sin embargo, las probabilidades de que encuentres tropiezos son de más de un 60%. Tropiezos, errores, fallos, "da error" conllevarán aprendizajes.

Referencias
===========

Borcard, D., & Legendre, P. (1994). Environmental control and spatial structure in ecological communities: An example using oribatid mites (acari, oribatei). *Environmental and Ecological Statistics*, *1*(1), 37–61.

Borcard, D., Legendre, P., & Drapeau, P. (1992). Partialling out the spatial component of ecological variation. *Ecology*, *73*(3), 1045–1055.
