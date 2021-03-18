---
output:
  pdf_document: default
  html_document: default
---
# (PART\*) Parte I: R básico {-}


# Logística de R {#chap:0}

R es un entorno de programación para el análisis estadístico y gráfico de datos muy popular, cada día más utilizado en empresas y universidades. Su uso  tiene muchas ventajas. Para empezar, es *software* libre. La elección de *software* libre es, en general, acertada por varios motivos. Por un lado,  transmite valores socialmente positivos, como por ejemplo la libertad individual, el conocimiento compartido, la solidaridad y la cooperación. Por otro, nos aproxima al método científico, porque permite el examen y mejora del código desarrollado por otros usuarios y la reproducibilidad de los resultados obtenidos. Finalmente, pero no menos importante desde un punto de vista práctico, podemos adquirir de manera legal y gratuita copias del programa, sin necesidad de licencias personales o académicas. 

Aparte de su faceta de *software* libre, R tiene algunas ventajas específicas: por ejemplo, su sintaxis básica es sencilla e intuitiva, con la que es muy fácil familiarizarse, lo que se traduce en un  aprendizaje  rápido y cómodo.  Además, tiene una enorme comunidad de usuarios, estructurada alrededor de  la *Comprehensive R Archive Network*, o  *CRAN*, que desarrolla cada día nuevos paquetes que extienden sus funcionalidades  y cubren casi todas las necesidades computacionales y estadísticas de un científico o ingeniero. Para que os hagáis una idea, en el momento de revisar estas notas (septiembre de 2019) el número de paquetes en el repositorio de la CRAN acaba de superar los 15000. 


## Cómo instalar R y *RStudio* 

 Instalar R es muy sencillo; de hecho, seguramente ya lo tenéis instalado en vuestro ordenador, pero es conveniente que dispongáis de su versión más reciente y que regularmente lo pongáis al día. Los pasos a realizar en  Windows o Mac OS X para instalar su última versión son los siguientes:

* Si sois usuarios de Windows, acceded a la página web de la  [*CRAN*](http://cran.r-project.org/) y pulsad sobre el enlace *Download R for Windows*. A continuación, entrad en el enlace *base*,  descargad R y seguid las instrucciones de instalación del  documento *Installation and other instructions* que encontraréis en esa  misma página. 

* Si sois usuarios de Mac OS X, acceded  a la página web de la  [*CRAN*](http://cran.r-project.org/) y pulsad sobre el enlace  *Download R for Mac OS X*. A continuación, descargad el fichero `.pkg`  correspondiente y, una vez descargado, abridlo y seguid las instrucciones del Asistente de Instalación.

* Si trabajáis con Ubuntu o Debian, para instalar  la última versión de R basta que ejecutéis en una terminal, estando conectados a Internet, la siguiente instrucción: 
```
sudo aptitude install r-base
```


Cuando instaláis R para Windows o Mac OS X, con él también se os instala una interfaz gráfica que se abrirá al abrir la aplicación y en la que podréis trabajar. La instalación para Linux no lleva una interfaz por defecto, así que sus usuarios  tienen que  trabajar con R en la terminal (ejecutando R para iniciar una sesión) o instalar aparte una interfaz.  Independientemente de todas estas posibilidades, en este curso usaremos  *RStudio* como interfaz gráfica de usuario de R para todos los sistemas operativos. 

Propiamente hablando, *RStudio* es mucho más que una interfaz de R: se trata de todo un entorno integrado para utilizar y programar con R, que dispone de un conjunto de herramientas que facilitan el trabajo con este lenguaje. Para instalarlo, se ha de descargar  del *url* [http://www.rstudio.com/products/rstudio/download/](http://www.rstudio.com/products/rstudio/download/) la versión correspondiente al sistema operativo en el que se trabaja; en cada caso, escoged la versión gratuita de *RStudio Desktop*. Una vez descargado, si usáis Windows o Mac OS X ya lo podéis abrir directamente. En el caso de Linux, hay que ejecutar en una terminal la siguiente instrucción para completar su instalación:
```
sudo dpkg -i rstudio-<version>-i386.deb
```
donde `version` refiere a la versión concreta que hayáis descargado.  Conviene  recordar que *RStudio* no es R, ni tan sólo lo contiene: hay que instalar ambos programas. De hecho, las instalaciones de R y *RStudio* son independientes una de la otra, de manera que cuando se pone al día uno de estos programas, no se modifica el otro.

\begin{figure}

{\centering \includegraphics[width=0.8\linewidth]{AprendeR-Parte-I_files/figure-html/rstudio1} 

}

\caption{Ventana de RStudio para Mac OS X.}(\#fig:rstudio1)
\end{figure}

Cuando se abre *RStudio*, aparece una ventana similar a la que  muestra la Figura   \@ref(fig:rstudio1): su apariencia exacta dependerá del sistema operativo, de la versión de *RStudio* e incluso de los paquetes que estemos usando.  De momento, nos concentraremos en la ventana de la izquierda,  llamada la **consola**  de R (la pestaña *Console*). Observaréis que en el momento de abrir la aplicación, dicha ventana contiene una serie de información (versión, 
créditos etc.) y al final una línea en blanco encabezada por el símbolo `>`. Este símbolo es la **marca de inicio**  e indica que R espera que escribáis alguna instrucción y la  ejecutéis.

Durante la mayor parte de este curso, usaremos *RStudio*  de manera interactiva: 

1. Escribiremos  una instrucción en la consola, a la derecha de la  marca de inicio de su última línea.
2. La ejecutaremos pulsando la tecla *Entrar* ($\hookleftarrow$).
3. R la evaluará y, si corresponde,  escribirá el resultado en la línea siguiente de la consola (como veremos, no todas las instrucciones hacen que R  escriba algo).
4. R abrirá una nueva línea en blanco encabezada por una marca de inicio, donde esperará una nueva instrucción. 

Haced una prueba: escribid `1+1` junto a la marca de inicio y pulsad *Entrar*;  R escribirá en la línea siguiente el resultado de la suma, `2`, y a continuación una nueva línea en blanco encabezada por la marca de inicio.
Ya hablaremos  en la Lección \@ref(chap:vect) del `[1]` que os habrá aparecido delante del 2 en el resultado. Hasta entonces, no os preocupéis por él. En los bloques de código de este libro no incluimos la marca de inicio, para que podáis copiar tranquilamente el código y luego pegarlo y ejecutarlo en vuestra consola, y el resultado aparece precedido de `##`, para que si por descuido copiáis un resultado, no se ejecute:  el símbolo `#` sirve para indicar a R que  no ejecute lo que venga a continuación en la misma línea. Así, en este libro el cálculo anterior corresponde a:

```r
1+1
#> [1] 2
```

Para facilitarnos el trabajo, la consola dispone de un mecanismo  para acceder a las instrucciones ya ejecutadas y modificarlas si queremos. Si situamos el cursor a la derecha de la marca de inicio de la línea inferior y pulsamos la tecla de la flecha vertical ascendente $\uparrow$, iremos obteniendo de manera consecutiva, en esa línea,  las instrucciones escritas hasta el momento en la misma sesión; si nos pasamos, podemos usar la tecla $\downarrow$ para retroceder dentro de esta lista; una vez alcanzada la instrucción deseada, podemos volver a ejecutarla o, con las teclas de flechas horizontales, ir al lugar de la instrucción que queramos y  reescribir un trozo antes de ejecutarla. Otra posibilidad es usar la pestaña *History* de la ventana superior derecha de *RStudio*, que contiene la lista de  todas las instrucciones que se han ejecutado en la sesión actual. Si seleccionamos una instrucción de esta lista y pulsamos  el botón *To console* del menú superior de la pestaña, la instrucción se copiará en la consola y la podremos modificar o ejecutar directamente.

También podemos copiar instrucciones de otros ficheros y pegarlas a la derecha de la marca de inicio de la manera habitual en el sistema operativo de nuestro ordenador. Pero hay que ir con cuidado: las instrucciones copiadas de ficheros en formato que no sea  texto simple  pueden contener caracteres invisibles a simple vista que generen errores al intentar ejecutar la instrucción copiada. En particular, esto afecta a las instrucciones que podáis copiar de ficheros en formato PDF, procurad no hacerlo. En cambio, no hay ningún problema en copiar y pegar instrucciones de ficheros html como los de estas lecciones. 

Volvamos a la ventana de *RStudio* de la Figura \@ref(fig:rstudio1). Observaréis que está dividida a su vez en tres ventanas. La de la izquierda es la consola, donde trabajamos en modo interactivo. La ventana inferior derecha tiene algunas pestañas, entre las que destacamos:

* *Files*, que muestra el contenido de la carpeta de trabajo actual (véase la Sección \@ref(sec:guardar)). Al hacer clic sobre un fichero en esta lista, se abrirá en la ventana de ficheros (véase la Sección \@ref(sec:guiones)).
* *Plots*, que muestra los gráficos que hayamos producido durante la sesión. Se puede navegar entre ellos con las flechas de la barra superior de la pestaña.
* *Packages*, que muestra todos los paquetes  instalados y, marcados, los que están cargados en la sesión actual (véase la Sección \@ref(sec:paquetes)).
* *Help*, donde aparecerá la ayuda que pidamos (véase la Sección \@ref(sec:help)).

Por lo que se refiere a la ventana superior izquierda, destacamos las dos pestañas siguientes:

* *Environment*, con la lista de los objetos actualmente definidos (véase la Lección \@ref(chap:calc)).
* *History*, de la que ya hemos hablado, que contiene la lista  de todas las instrucciones que hayamos ejecutado durante la sesión.

Aparte de estas tres ventanas, *RStudio* dispone de una cuarta ventana para ficheros, que se abre en el sector superior izquierdo, sobre la consola (véase la Sección \@ref(sec:guiones)).

Para cerrar *RStudio*, basta  elegir *Quit RStudio*  del menú *RStudio*  o 
pulsar la combinación de teclas usual para cerrar un programa en vuestro sistema operativo.


## Cómo guardar el trabajo realizado {#sec:guardar}

 Antes de empezar a utilizar R  en serio, lo primero que tenéis que hacer es crear en vuestro ordenador una carpeta específica que será  vuestra **carpeta de trabajo**  con R. A continuación, en las *Preferencias*  de *RStudio*, que podréis abrir desde el menú  *RStudio*, tenéis que declarar esta carpeta como *Default working directory*. A partir de este momento, por defecto, todo el trabajo que realicéis quedará guardado dentro de esta carpeta, y  *RStudio* buscará dentro de esta carpeta todo lo que queráis que lea. 
Si en un momento determinado queréis cambiar temporalmente de carpeta de trabajo, tenéis dos opciones:

* Podéis usar el menú *Session* $\rightarrow$ *Set Working Directory* $\rightarrow$ *Choose Directory...* para escoger una carpeta. 

* Podéis abrir la pestaña *Files* de la ventana inferior derecha y navegar por el árbol de directorios  que aparece en su barra superior hasta llegar a la carpeta deseada.

Tanto de una manera como de la otra, la carpeta que especifiquéis será la carpeta de trabajo durante lo que queda de sesión o hasta que la volváis a cambiar.

En cualquier momento podéis guardar la sesión en la que estéis trabajando usando el menú *Session* $\rightarrow$ *Save Workspace as...*.
Además, si no habéis modificado esta opción en las *Preferencias*, cuando cerréis *RStudio* se os pedirá si queréis guardar la sesión; si contestáis que sí, *RStudio*  guardará en la carpeta de trabajo dos ficheros, `.RData` y `.RHistory`, que se cargarán automáticamente al volver a abrir *RStudio* y estaréis exactamente donde lo habíais dejado. Nuestro consejo es que digáis que no: normalmente, no os interesará arrastrar todo lo que hayáis hecho en sesiones anteriores. Y si queréis guardar algunas definiciones e instrucciones de una sesión, lo más práctico es guardarlas en un *guión* (véase la Sección \@ref(sec:guiones)).

Los gráficos que generéis con *RStudio* aparecerán en la ventana inferior derecha, en la pestaña *Plots* que se activa  automáticamente cuando se crea alguno. La apariencia del gráfico dependerá de las dimensiones de esta ventana, por lo que es conveniente que sea cuadrada si queréis que el gráfico no aparezca achatado o estirado. Si modificáis la forma de la ventana, las dimensiones del gráfico que aparezca en ella se modificarán de manera automática.

Para guardar un gráfico, hay que ir al menú *Export* de esta pestaña y seleccionar cómo queréis guardarlo: como una imagen en uno los formatos estándares de imágenes (.png, .jpeg, .tiff, etc.) o en formato PDF. Entonces, se abrirá una ventana donde podéis darle nombre, modificar sus dimensiones y especificar el directorio donde queráis que se guarde, entre otras opciones.


## Cómo trabajar con guiones y otros ficheros {#sec:guiones}

 R admite la posibilidad de crear y usar ficheros de instrucciones que se pueden ejecutar y guardar llamados **guiones**  (*scripts*). Estos guiones son una alternativa muy cómoda a las sesiones interactivas, porque permiten guardar las versiones finales de las instrucciones usadas, y no toda la sesión con pruebas, errores y resultados provisionales, y  facilitan la ejecución de secuencias de instrucciones en un solo paso. Además, un guión se puede guardar, volver a abrir más adelante, editar, etc.  Como ya hemos comentado, el símbolo `#` sirve para indicar a R que omita todo lo que hay a su derecha en la misma línea, lo que permite añadir comentarios a un guión.


Para crear un guión con *RStudio*, tenéis que ir al menú *File* $\rightarrow$ *New File* $\rightarrow$ *R Script*. Veréis que os aparece una ventana nueva  en el sector superior izquierdo de la ventana de *RStudio*, sobre la consola: la llamaremos **ventana de ficheros**. En ella podéis escribir, línea a línea, las instrucciones que queráis. Para ejecutar  instrucciones de esta ventana,  basta que las seleccionéis y pulséis el botón *Run* que aparece en la barra superior  de esta ventana.


Para guardar un guión, basta pulsar el botón con el icono de un disquete de ordenador que aparece en la barra superior de su ventana. Otra posibilidad es usar el menú *File* $\rightarrow$ *Save*, o pulsar la combinación de teclas usual para guardar un fichero en vuestro sistema operativo, siempre y cuando la **ventana activa**  de *RStudio* (donde esté activo el cursor en ese momento) sea la del guión. Al guardar un guión por primera vez,  se abre una ventana de diálogo donde *RStudio* espera que le demos un nombre; la costumbre es usar para los guiones la extensión `.R`.
 
Podéis abrir un guión ya preexistente con *RStudio*  usando el menú *File* $\rightarrow$ *Open File* de *RStudio* o pulsando sobre él en la pestaña *Files*. También podéis arrastrar el icono del guión sobre el de *RStudio* o (si habéis declarado que la aplicación por defecto para abrir ficheros con extensión  `.R` sea *RStudio*) simplemente abrir el fichero de la manera usual en vuestro sistema operativo.
 
Además de guiones, con *RStudio* también podemos crear otros tipos de ficheros que combinen instrucciones de R con instrucciones de otro lenguaje. En este curso lo usaremos para crear ficheros *R Markdown*, que permiten generar de manera muy cómoda informes y presentaciones que incorporen instrucciones de R (o sólo sus resultados). Para crear un fichero *R Markdown*, tenéis que ir al menú *File* $\rightarrow$ *New File* $\rightarrow$ *R Markdown...*, donde os aparecerá una ventana que os pedirá el tipo de documento (*Document*, *Presentation*...), su título  y el formato de salida.  Una vez completada esta información, se abrirá el fichero en la ventana superior izquierda. 

Por poner un ejemplo, supongamos que habéis elegido realizar un informe (*Document*) con formato de salida html (los formatos posibles son: PDF, HTML o Word); entonces, para  generar un informe básico  basta sustituir las palabras clave que  ha generado *RStudio* en esta ventana. Probadlo: cambiad el título y el texto; a continuación, guardad el fichero con el nombre que queráis y extensión `.Rmd`, y pulsad el botón *Knit* situado en la barra superior de la ventana; se generará un fichero HTML en la carpeta de trabajo, con el texto del fichero *R Markdown* y el mismo título cambiando la extensión  `.Rmd` por  `.html`, y se abrirá en una ventana aparte.

Aprender los primeros pasos de   *R Markdown* es sencillo. Para ello, podéis consultar el manual de referencia rápida de  *R Markdown*  que encontraréis en el menú *Help* de *RStudio*, que para la mayoría de ejercicios de este curso es más que suficiente.
También os puede ser útiles  las "chuletas"  de  *R Markdown*   siguientes:

* [https://www.rstudio.com/wp-content/uploads/2015/03/rmarkdown-reference.pdf](https://www.rstudio.com/wp-content/uploads/2015/03/rmarkdown-reference.pdf)

* [https://github.com/rstudio/cheatsheets/raw/master/rmarkdown-2.0.pdf](https://github.com/rstudio/cheatsheets/raw/master/rmarkdown-2.0.pdf) 

* [https://www.rstudio.com/wp-content/uploads/2015/02/rmarkdown-cheatsheet.pdf](https://www.rstudio.com/wp-content/uploads/2015/02/rmarkdown-cheatsheet.pdf)

En la Lección \@ref(chap:Rmd)  explicamos algunas técnicas para mejorar los ficheros resultantes.


## Cómo obtener ayuda {#sec:help}

Para conocer toda la información (qué hace, cuál es la sintaxis correcta, qué parámetros tiene, algunos ejemplos de uso...) sobre una función o un objeto, se puede usar el campo de búsqueda, marcado con una lupa, en la esquina superior derecha de la pestaña de **Ayuda** (*Help*), situada en la ventana inferior derecha de *RStudio*. Como alternativa, se pueden usar las instrucciones


```r
help(nombre del objeto)
```
o, equivalentemente, 

```r
?nombre del objeto
```



Por ejemplo, si entramos  en el campo de búsqueda de la pestaña de Ayuda la palabra `sum`, o si **entramos** en la consola (es decir, si escribimos a la derecha de la marca de inicio y a continuación pulsamos la tecla *Entrar*)    la instrucción


```r
help(sum)
```
 obtenemos en la pestaña de Ayuda toda la información sobre la función `sum`.

Cuando hayamos avanzado un poco en este curso, la Ayuda os será muy útil.  Aquí sólo veremos alguna aplicación simple de la mayoría de las funciones que estudiemos, con los parámetros más importantes y suficientes para nuestros propósitos, y necesitaréis consultar su Ayuda para conocer todos sus usos, todos sus parámetros u otra información relevante. 

Si queremos pedir ayuda sobre un tema concreto, pero no sabemos el nombre exacto de la función, podemos entrar una palabra clave en el campo de búsqueda de la  pestaña de Ayuda, o usar la función 

```r
help.search("palabra clave")
```
o, equivalentemente, 

```r
??"palabra clave"
```
(las comillas ahora son obligatorias). De esta manera, conseguiremos en la ventana de Ayuda una lista de las funciones que R entiende que están relacionadas con la palabra clave entrada. Entonces, pulsando en la función que nos interese de esta lista, aparecerá la información específica sobre ella.
Como podéis imaginar, conviene que la palabra clave esté en inglés.

Además de la ayuda que incorpora el mismo R, siempre podéis acudir a foros y listas de discusión para encontrar ayuda sobre cualquier duda que podáis tener. Algunos recursos que nosotros encontramos especialmente útiles son los siguientes:

* La sección dedicada a R del foro [*stackoverflow*](http://stackoverflow.com/questions/tagged/r) 
* El archivo de la lista de discusión  [*R-help*](http://r.789695.n4.nabble.com/r-help-f789696.html) 
* El grupo de Facebook [*R project en español*](https://www.facebook.com/groups/rprojectsp) 

Si tenéis alguna dificultad, es muy probable que alguien ya la haya tenido y se la hayan  resuelto en alguno de estos foros. 

Existe también una comunidad muy activa de usuarios hispanos de R, en cuyo [portal web](http://r-es.org/Comunidad) encontraréis muchos recursos útiles para mejorar vuestro conocimiento de este lenguaje.


## Cómo instalar y cargar paquetes {#sec:paquetes}

Muchas funciones y tablas de datos útiles no vienen con la instalación básica de R, sino que forman parte de **paquetes** (*packages*), que se tienen que instalar y cargar para poderlos usar. Por citar un par de ejemplos, el paquete **magic** lleva una función `magic` que crea **cuadrados mágicos** (tablas cuadradas de números naturales diferentes dos a dos tales que las sumas de todas sus columnas,  de todas sus filas y  de sus dos diagonales principales valgan todas lo mismo), y para usarla tenemos que instalar y cargar este paquete. De manera similar,  el paquete **ggplot2** incorpora una serie  de funciones para dibujar gráficos avanzados que no podemos usar si primero no instalamos y cargamos este paquete.

Podemos consultar en la pestaña  *Packages*  la lista de paquetes que tenemos instalados. Los paquetes que aparecen marcados en esta lista son los que  tenemos  cargados en la sesión actual. Si queremos cargar un paquete ya instalado, basta marcarlo en esta lista; podemos hacerlo también desde la consola, con la instrucción 

```r
library(nombre del paquete)
```

En caso de necesitar un paquete que no tengamos instalado, hay que instalarlo antes de poderlo cargar. La mayoría de los paquetes se pueden instalar desde el repositorio del CRAN; esto se puede hacer de dos maneras:

* Desde la consola, entrando la instrucción 

```r
install.packages("nombre del paquete", dep=TRUE)
```
(las comillas son obligatorias, y fijaos en el plural de `packages` aunque sólo queráis instalar uno). El parámetro `dep=TRUE` hace que R instale no sólo el paquete requerido, sino todos aquellos de los que dependa para funcionar correctamente. 

* Pulsando el botón *Install* de la barra superior de la pestaña de paquetes; al hacerlo, *RStudio* abre una ventana dónde se nos pide el nombre del paquete a instalar. Conviene dejar marcada la opción *Install dependencies*, para que se instalen también los paquetes necesarios para su funcionamiento.

Así, supongamos que queremos construir cuadrados mágicos, pero aún no hemos cargado el paquete `magic`.


```r
magic(10)
#> Error in magic(10): no se pudo encontrar la función "magic"
```

Así que instalamos y cargamos dicho paquete (también lo podríamos hacer desde la ventana *Packages*):

```r
install.packages("magic", dep=TRUE)
library(magic)
```



Ahora ya podemos usar la función `magic`:


```r
magic(10)
#>       [,1] [,2] [,3] [,4] [,5] [,6] [,7] [,8] [,9] [,10]
#>  [1,]   34   35    6    7   98   99   70   71   42    43
#>  [2,]   36   33    8    5  100   97   72   69   44    41
#>  [3,]   11   10   83   82   75   74   47   46   39    38
#>  [4,]   12    9   84   81   73   76   48   45   40    37
#>  [5,]   87   86   79   78   51   50   23   22   15    14
#>  [6,]   85   88   77   80   52   49   21   24   13    16
#>  [7,]   63   62   55   54   27   26   19   18   91    90
#>  [8,]   61   64   53   56   25   28   17   20   89    92
#>  [9,]   59   58   31   30    3    2   95   94   67    66
#> [10,]   57   60   29   32    1    4   93   96   65    68
```

Cuando cerramos *RStudio*, los paquetes instalados en la sesión siguen instalados, pero los cargados se pierden; por lo tanto, si queremos volver a usarlos en otra sesión, tendremos que volver a cargarlos.

Hay paquetes que no se encuentran en el CRAN y que, por lo tanto, no se pueden instalar de la forma que hemos visto. Cuando sea necesario, ya explicaremos la manera de instalarlos y cargarlos en cada caso. 

Para terminar, observad que a la derecha del nombre de cada paquete en la pestaña *Packages* aparecen dos símbolos. Al pulsar el primero, seis puntitos, se abrirá en el navegador la página de información del paquete, y al pulsar el segundo, una crucecita, desinstalamos el paquete. Asimismo, en la barra superior de la pestaña *Packages* encontraréis un botón *Update* que sirve para poner al día  los paquetes instalados, obteniendo sus últimas versiones publicadas.

## Guía rápida

* `help` o `?` permiten pedir información sobre una función. También se puede usar el campo de búsqueda de la pestaña *Help* en la ventana inferior derecha de *RStudio*.
* `help.search` o `??` permiten pedir información sobre una palabra clave (entrada entre comillas). De nuevo, también se puede usar el campo de búsqueda de la pestaña *Help* en la ventana inferior derecha de *RStudio*.
* `install.packages("paquete", dep=TRUE)` instala el `paquete` y todos los otros paquetes de los que dependa. También se puede usar el botón *Install* de la pestaña *Packages* en la ventana inferior derecha de *RStudio*.
* `library(paquete)` carga el `paquete`. También se puede cargar marcándolo en la ventana *Packages*  de *RStudio*.
