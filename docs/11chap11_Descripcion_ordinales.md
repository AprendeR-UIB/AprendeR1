---
output:
  pdf_document: default
  html_document: default
---
# Descripción de datos ordinales {#chap:ord}

Los datos ordinales son parecidos a los cualitativos, en el sentido de que son cualidades de objetos o individuos. Su diferencia con los datos cualitativos está en que las características que expresan los datos ordinales tienen un orden natural que permite *acumular*  observaciones, es decir, contar cuántas hay por debajo de cada nivel. Un caso frecuente son las escalas tipo *Likert*, que se usan para conocer la opinión de un grupo de personas sobre un tema determinado; para más información, podéis consultar  [la entrada de la Wikipedia sobre escalas Likert](http://es.wikipedia.org/wiki/Escalas_Likert).


## Frecuencias para datos ordinales

 Cuando trabajamos con datos ordinales, el orden de los niveles de los datos permite calcular no sólo las frecuencias absolutas y relativas que veíamos en la lección anterior, y que para variables ordinales se definen del mismo modo, sino también frecuencias **acumuladas**. Es decir, no sólo podemos contar cuántas veces hemos observado un cierto dato, sino también cuántas veces hemos observado un dato menor o igual que él.

\BeginKnitrBlock{example}
<span class="example" id="exm:ex1701bis"><strong>(\#exm:ex1701bis) </strong></span>Tenemos una muestra de 20 estudiantes de quienes sabemos la calificación que han sacado en un examen. Clasificamos estas calificaciones en Suspenso (*S*), Aprobado (*A*), Notable (*N*) y Sobresaliente (*E*) y consideramos su orden natural *S* < *A* < *N* < *E*. Las calificaciones que han obtenido son las siguientes:
<p style="text-align:center">*A*, *A*, *N*, *S*, *S*, *A*, *N*, *E*, *A*, *A*, *S*, *S*, *S*, *A*, *E*, *N*, *N*, *E*, *S*, *A*.</p> 
  
  
  
\EndKnitrBlock{example}
En esta lista hay 6 *S*, 7 *A*, 4 *N* y 3 *E*: éstas serían las frecuencias absolutas de las calificaciones en esta muestra de estudiantes. Por lo que se refiere a sus **frecuencias absolutas acumuladas**:

* Hay 6 estudiantes que han obtenido *S* o menos: la frecuencia absoluta acumulada de *S* es 6.
* Hay 13 estudiantes que han obtenido *A* o menos (6 *S* y 7 *A*): la frecuencia absoluta acumulada de *A* es 13.
* Hay 17 estudiantes que han obtenido *N* o menos (6 *S*, 7 *A* y 4 *N*): la frecuencia absoluta acumulada de *N* es 17.
* Hay 20 estudiantes que han obtenido *E* o menos (todos): la frecuencia absoluta acumulada de *E* es 20.

La **frecuencia relativa acumulada**  de cada calificación es la fracción del total de estudiantes que representa su frecuencia absoluta acumulada: por ejemplo, la frecuencia relativa acumulada de notables es la proporción de estudiantes que han sacado  un notable o menos, y, por lo tanto, es igual a la frecuencia absoluta acumulada de *N* dividida por el número total de estudiantes. Así pues, para calcular las frecuencias relativas acumuladas de las calificaciones en esta muestra, tenemos que dividir sus frecuencias absolutas acumuladas entre 20:

* *S*: 6/20=0.3
* *A*: 13/20=0.65
* *N*: 17/20=0.85
* *E*:  20/20=1

En general, supongamos que efectuamos $n$ observaciones
$$
x_1,x_2,\ldots,x_n
$$
de un cierto tipo de datos ordinales, cuyos posibles   **niveles**  ordenados son
$$
l_1<l_2<\cdots <l_k.
$$
Por lo tanto, cada una de estas observaciones $x_j$ es igual a algún $l_i$. Diremos que estas observaciones forman una **variable ordinal**. En el ejemplo anterior, tendríamos que los niveles ordenados son *S* < *A* < *N* < *E*, que  $n=20$, y que $x_1,\ldots,x_{20}$ son las calificaciones obtenidas por los estudiantes de la muestra.

Con estas notaciones:

* Las definiciones de **frecuencias absolutas**  $n_j$ y **relativas**  $f_j$, para cada nivel $l_j$, 
son las mismas que en una variable cualitativa (véase la Sección \@ref(sec:edqual)). 

* La **frecuencia absoluta acumulada** del nivel $l_j$ en esta variable ordinal  es el número $N_j$ de observaciones $x_i$ tales que $x_i\leq l_j$. Es decir,
es 
$$N_j=\sum\limits_{k=1}^j n_k.$$

* La **frecuencia relativa acumulada** del nivel $l_j$ en esta variable ordinal  es la fracción (en tanto por uno) $F_j$ de observaciones $x_i$ tales que $x_i\leq l_j$. Es decir, 
$$
F_j=\dfrac{N_j}{n}=\sum\limits_{k=1}^j f_k.
$$ 



## Descripción de datos ordinales con R

 Recordemos de la Lección \@ref(chap:vect) que la función `cumsum`, aplicada a un vector, calcula el vector de sus sumas acumuladas. Sobre una tabla de contingencia tiene el mismo efecto, y por lo tanto podemos usarla para calcular la tabla de frecuencias acumuladas (absolutas o relativas) de un vector, aplicándola a su tabla de frecuencias (absolutas o relativas, según corresponda). 


\BeginKnitrBlock{example}
<span class="example" id="exm:ex1ordinales"><strong>(\#exm:ex1ordinales) </strong></span>Vamos a calcular y representar gráficamente las frecuencias acumuladas de la muestra de calificaciones del Ejemplo \@ref(exm:ex1701bis). Para ello entraremos dichas calificaciones como un factor ordenado, porque es la manera natural de guardar una variable ordinal en R.



\EndKnitrBlock{example}


```r
notas=ordered(c("A","A","N","S","S","A","N","E","A","A","S","S","S","A","E","N","N","E","S","A"), 
              levels=c("S","A","N","E"))
notas
#>  [1] A A N S S A N E A A S S S A E N N E S A
#> Levels: S < A < N < E
```

* Su tabla de frecuencias absolutas:


```r
table(notas)
#> notas
#> S A N E 
#> 6 7 4 3
```

* Su tabla de frecuencias absolutas acumuladas:


```r
cumsum(table(notas))
#>  S  A  N  E 
#>  6 13 17 20
```

* Su tabla de frecuencias relativas acumuladas:


```r
cumsum(prop.table(table(notas)))
#>    S    A    N    E 
#> 0.30 0.65 0.85 1.00
```

* Un diagrama de barras de sus frecuencias absolutas:


```r
barplot(table(notas))
```



\begin{center}\includegraphics[width=0.9\linewidth]{11chap11_Descripcion_ordinales_files/figure-latex/unnamed-chunk-5-1} \end{center}

* Un diagrama de barras de sus frecuencias absolutas acumuladas:


```r
barplot(cumsum(table(notas)))
```



\begin{center}\includegraphics[width=0.9\linewidth]{11chap11_Descripcion_ordinales_files/figure-latex/unnamed-chunk-6-1} \end{center}


<!--
```{r F1702,fig.cap="Diagramas de barras de frecuencias absolutas y de frecuencias absolutas acumuladas de las notas del Ejemplo 
\@ref(ex:ex1701bis)."}
knitr::include_graphics(c("images/notasnoacum1.png","images/notasacum1.png"))
```


\begin{figure}[htb]
\begin{center}
\includegraphics[width=0.45\textwidth]{notasnoacum1.pdf}\
\includegraphics[width=0.45\textwidth]{notasacum1.pdf}
\end{center}
\caption{Diagramas de barras de frecuencias absolutas y de frecuencias absolutas acumuladas de las notas del Ejemplo \@ref(ex:17.1).}\label{fig:17.2)
\end{figure}
-->

Para calcular las frecuencias relativas acumuladas hemos usado la instrucción 

```r
cumsum(prop.table(table(notas)))
```
que va sumando las frecuencias relativas. También las podríamos  haber calculado dividiendo las frecuencias 
absolutas acumuladas por el número de datos, usando una de las dos instrucciones siguientes:

```r
cumsum(table(notas))/length(notas)
#>    S    A    N    E 
#> 0.30 0.65 0.85 1.00
cumsum(table(notas)/length(notas))
#>    S    A    N    E 
#> 0.30 0.65 0.85 1.00
```
Pero *no* podíamos usar 


```r
prop.table(cumsum(table(notas)))
#>         S         A         N         E 
#> 0.1071429 0.2321429 0.3035714 0.3571429
```
Pensad qué ha entendido R que queríamos hacer con esta última instrucción.

\BeginKnitrBlock{example}
<span class="example" id="exm:ex1704"><strong>(\#exm:ex1704) </strong></span>En un estudio sobre el comportamiento ético de una empresa, a un grupo de técnicos en impacto ambiental que trabajaban en dicha empresa se les hizo la pregunta siguiente: "*¿Cree que su empresa anima a sus técnicos en impacto ambiental a usar métodos que favorezcan la opinión del cliente que ha encargado el estudio?*"
  

\EndKnitrBlock{example}

Las posibles respuestas eran las que aparecen en la Tabla \@ref(tab:Likert), y forman una escala ordinal de tipo \emph{Likert}, con 1 < 2 < 3 < 4 < 5.

\begin{table}

\caption{(\#tab:Likert)Un ejemplo de escala *Likert*.}
\centering
\begin{tabular}[t]{rl}
\toprule
Nivel & Significado\\
\midrule
1 & Muy en desacuerdo\\
2 & En desacuerdo\\
3 & Neutro\\
4 & De acuerdo\\
5 & Muy de acuerdo\\
\bottomrule
\end{tabular}
\end{table}


<!--
\begin{table}[h]
\begin{center}
\abovecaptionskip=7pt
\begin{tabular}{|r|l|}
\hline
Nivel & Significado\\\hline
1 & Muy en desacuerdo\\
2 & En desacuerdo \\
3 & Neutro\\
4 & De acuerdo\\
5 & Muy de acuerdo\\\hline
\end{tabular}
\caption{Un ejemplo de datos ordinales.}\label{tablaLikert}
\end{center}
\end{table}
-->

Supongamos que se recogieron las siguientes respuestas de 100 técnicos, que tenemos en un vector:

```r
respuestas=c(4,4,2,1,3,3,4,1,1,3,5,2,5,2,1,2,3,2,1,1,2,2,4,2,1,
             1,1,2,4,5,3,4,2,2,4,4,3,1,3,3,2,1,5,4,1,2,2,3,3,3,
             1,4,3,5,1,5,1,2,5,5,2,4,5,1,4,3,1,1,4,3,3,4,4,1,2,
             1,3,4,1,4,2,2,4,1,3,5,3,3,3,2,2,3,3,3,2,4,1,1,4,3)
```


En este caso tenemos 5 niveles ($k=5$) y 100 observaciones ($n=100$) que forman una variable ordinal que llamamos *respuestas*. Vamos a calcular sus dos tablas de frecuencias relativas (acumuladas o no) y dos diagramas de barras adecuados de sus frecuencias relativas (de nuevo, acumuladas o no). Para ello, en primer lugar transformaremos este vector en un factor ordenado.


```r
respuestas=ordered(respuestas,levels=1:5)
```

* Su tabla de frecuencias relativas:


```r
prop.table(table(respuestas))
#> respuestas
#>    1    2    3    4    5 
#> 0.24 0.22 0.24 0.20 0.10
```

* Su tabla de frecuencias relativas acumuladas:


```r
cumsum(prop.table(table(respuestas)))
#>    1    2    3    4    5 
#> 0.24 0.46 0.70 0.90 1.00
```

* Un diagrama de barras de sus frecuencias relativas:


```r
Nombres.compl=c("Muy en\n desacuerdo","En\n desacuerdo","Neutro\n ",
                "De\n acuerdo","Muy de\n acuerdo")
barplot(prop.table(table(respuestas)), ylim=c(0, 0.30), cex.names=0.75,
  main="Diagrama de barras de las frecuencias relativas\n de la variable \"respuestas\"", 
  names=Nombres.compl, xlab="Nivel de acuerdo escala Likert",  ylab="Frec. relativas")
```



\begin{center}\includegraphics[width=0.9\linewidth]{11chap11_Descripcion_ordinales_files/figure-latex/unnamed-chunk-14-1} \end{center}

* Un diagrama de barras de sus frecuencias relativas acumuladas:


```r
barplot(cumsum(prop.table(table(respuestas))), ylim=c(0, 1), cex.names=0.75,
  main="Diagrama de barras de las frecuencias relativas acumuladas \n de la variable \"respuestas\"", 
  names=Nombres.compl, xlab="Nivel de acuerdo escala Likert", ylab="Frec. relativas acumuladas")
```



\begin{center}\includegraphics[width=0.9\linewidth]{11chap11_Descripcion_ordinales_files/figure-latex/unnamed-chunk-15-1} \end{center}


En los dos últimos diagramas de barras, hemos representado los niveles con un texto más descriptivo. Para hacerlo, hemos definido un vector `Nombres.compl` con sus nuevos nombres en el orden correspondiente (y en dos líneas  cada uno para ocupar menos espacio horizontal), y entonces en los `barplot` hemos especificado `names=Nombres.compl`. Además, con el parámetro `cex.names` hemos reducido un 25% el tamaño de los nombres de las barras para que cupieran bien en el dibujo.


\BeginKnitrBlock{example}
<span class="example" id="exm:ex1706"><strong>(\#exm:ex1706) </strong></span>Un microbiólogo ha evaluado la semejanza a una cierta comunidad prototipo de los microbiotas intestinales de 40 individuos con síndrome del colon irritable. Los niveles de semejanza que ha usado son los de la Tabla \@ref(tab:tablameta), y los considera ordenados de la  manera natural:
  
  
\EndKnitrBlock{example}

<p style="text-align:center">Tot.difs <Difs < Pars < Muy.pars < Iguales</p>


\begin{table}

\caption{(\#tab:tablameta)Niveles de semejanza de comunidades microbianas.}
\centering
\begin{tabular}[t]{ll}
\toprule
Nivel & Significado\\
\midrule
Tot.difs & Totalmente diferentes\\
Difs & Diferentes\\
Pars & Parecidas\\
Muy.pars & Muy parecidas\\
Iguales & Totalmente Iguales\\
\bottomrule
\end{tabular}
\end{table}


<!--
\begin{table}[h]
\begin{center}
\abovecaptionskip=6pt
\begin{tabular}{|r|l|}
\hline
Nivel & Significado\\\hline
`Tot.difs` & Totalmente diferentes\\
`Difs` & Diferentes \\
`Pars` & Parecidas \\
`Muy.pars` & Muy parecidas\\
`Iguales` & Totalmente iguales\\\hline
\end{tabular}
\caption{Niveles de semejanza de comunidades microbianas.}\label{tablameta}
\end{center}
\end{table}
-->

Los valores obtenidos en el estudio son los contenidos en el siguiente vector.


```r
datos=c("Difs","Pars","Difs","Muy.pars","Muy.pars","Muy.pars","Iguales","Pars","Difs","Tot.difs",
        "Muy.pars","Iguales","Muy.pars","Pars","Pars","Muy.pars","Iguales","Difs","Difs","Pars",
        "Muy.pars","Muy.pars","Muy.pars","Difs","Pars","Pars","Iguales","Iguales","Muy.pars",
        "Iguales","Difs","Tot.difs","Pars","Muy.pars","Iguales","Difs","Muy.pars","Muy.pars",
        "Iguales","Tot.difs")
```

Para estudiar las frecuencias acumuladas de los niveles de semejanza en este estudio, transformaremos este vector en un factor ordenado con los niveles ordenados de manera adecuada.


```r
sem.com=ordered(datos,levels=c("Tot.difs","Difs","Pars","Muy.pars","Iguales"))
```

* La tabla de frecuencias absolutas:


```r
AbsFr=table(sem.com)
AbsFr
#> sem.com
#> Tot.difs     Difs     Pars Muy.pars  Iguales 
#>        3        8        8       13        8
```

* La tabla de frecuencias relativas:


```r
prop.table(AbsFr)
#> sem.com
#> Tot.difs     Difs     Pars Muy.pars  Iguales 
#>    0.075    0.200    0.200    0.325    0.200
```

* La tabla de frecuencias absolutas acumuladas:


```r
cumsum(AbsFr)
#> Tot.difs     Difs     Pars Muy.pars  Iguales 
#>        3       11       19       32       40
```

* La tabla de frecuencias relativas acumuladas:


```r
cumsum(prop.table(AbsFr))
#> Tot.difs     Difs     Pars Muy.pars  Iguales 
#>    0.075    0.275    0.475    0.800    1.000
```

* Un diagrama de barras de sus frecuencias relativas acumuladas:


```r
Nombres.Completos=c("Totalmente\n diferentes","Diferentes\n","Parecidas\n ",
                    "Muy\n parecidas","Totalmente\n iguales")
barplot(cumsum(prop.table(AbsFr)), names=Nombres.Completos, ylim=c(0, 1), cex.names=0.75)
```



\begin{center}\includegraphics[width=0.9\linewidth]{11chap11_Descripcion_ordinales_files/figure-latex/unnamed-chunk-21-1} \end{center}


Para calcular frecuencias acumuladas en una tabla multidimensional, hay que aplicar a la tabla la función `cumsum` mediante la función `apply`. En este caso concreto, la sintaxis de la instrucción sería 

```r
apply(tabla, MARGIN=..., FUN=cumsum)
```
donde el valor de `MARGIN` ha de ser el de la dimensión en la que queremos acumular las frecuencias: 1 si queremos calcular las frecuencias acumuladas por filas,  2 si las queremos calcular por columnas, etc.  Esta construcción tiene algunas particularidades, que vamos a ilustrar con un ejemplo.

<!--
\begin{ejemplo}\label{ex:encuestacum}
-->


\BeginKnitrBlock{example}
<span class="example" id="exm:encuestacum"><strong>(\#exm:encuestacum) </strong></span>Supongamos que las 100 respuestas a la encuesta en el Ejemplo \@ref(exm:ex1704) en realidad provienen de técnicos de tres empresas diferentes, A, B y C, de manera que las 30 primeras son de técnicos de A, las 20 siguientes, de técnicos de B, y las 50 últimas, de técnicos de C. Nos interesa estudiar la distribución de las respuestas según la empresa. 


\EndKnitrBlock{example}

Vamos a organizar estos datos en un *data frame*. Para que sea  más fácil visualizar la información que nos interesa, es conveniente que las filas  de las tablas de frecuencias correspondan a las empresas. Por lo tanto, al definir el *data frame*, entraremos como primera variable la de las empresas; de esta manera, éstas aparecerán en las filas al aplicarle la función `table`. Recordad además que las respuestas ya las tenemos convenientemente organizadas  en un factor ordenado llamado *respuestas*.



```r
empresas=rep(c("A","B","C"), times=c(30,20,50))
df_encuesta=data.frame(empresas,respuestas)
str(df_encuesta)
#> 'data.frame':	100 obs. of  2 variables:
#>  $ empresas  : chr  "A" "A" "A" "A" ...
#>  $ respuestas: Ord.factor w/ 5 levels "1"<"2"<"3"<"4"<..: 4 4 2 1 3 3 4 1 1 3 ...
head(df_encuesta,5)
#>   empresas respuestas
#> 1        A          4
#> 2        A          4
#> 3        A          2
#> 4        A          1
#> 5        A          3
table(df_encuesta)
#>         respuestas
#> empresas  1  2  3  4  5
#>        A  9  9  4  5  3
#>        B  3  5  7  4  1
#>        C 12  8 13 11  6
```


Para calcular la tabla de frecuencias absolutas acumuladas de las respuestas por empresa, y como las empresas definen las filas de la tabla anterior, hemos de usar `apply` con `MARGIN=1`.


```r
apply(table(df_encuesta), MARGIN=1, FUN=cumsum)
#>           empresas
#> respuestas  A  B  C
#>          1  9  3 12
#>          2 18  8 20
#>          3 22 15 33
#>          4 27 19 44
#>          5 30 20 50
```
¡La tabla se ha traspuesto!
Resulta que cuando se aplica `apply` a una `table` bidimensional, R intercambia,  si es necesario, filas por columnas en el resultado para que la dimensión de la tabla resultante en la que se haya aplicado la función sea la de las columnas. Por lo tanto, para volver a tener las empresas en las filas, hemos de trasponer el resultado de `apply`.


```r
t(apply(table(df_encuesta), MARGIN=1, FUN=cumsum))
#>         respuestas
#> empresas  1  2  3  4  5
#>        A  9 18 22 27 30
#>        B  3  8 15 19 20
#>        C 12 20 33 44 50
```


Vamos ahora a calcular la tabla de frecuencias relativas acumuladas de las respuestas por empresa. Para ello, y en una sola instrucción, primero calculamos la tabla de frecuencias relativas por filas; a continuación, las acumulamos por filas con `apply` y `cumsum`; y, finalmente, como ya estamos avisados, trasponemos el resultado. Además, redondearemos el resultado a 3 cifras decimales.


```r
round(t(apply(prop.table(table(df_encuesta), margin=1), MARGIN=1, FUN=cumsum)),3)
#>         respuestas
#> empresas    1   2     3    4 5
#>        A 0.30 0.6 0.733 0.90 1
#>        B 0.15 0.4 0.750 0.95 1
#>        C 0.24 0.4 0.660 0.88 1
```


Vamos ahora a dibujar el diagrama de barras por bloques de esta tabla. Como queremos que las barras  de este diagrama se agrupen por empresas, hemos de aplicar `barplot` a la tabla sin trasponer.


```r
Tabla=apply(prop.table(table(df_encuesta), margin=1), MARGIN=1,FUN=cumsum)
barplot(Tabla, beside=TRUE, legend=TRUE,
        main="Diagrama de barras de frecuencias relativas acumuladas\n de respuestas por empresa")
```



\begin{center}\includegraphics[width=0.9\linewidth]{11chap11_Descripcion_ordinales_files/figure-latex/unnamed-chunk-27-1} \end{center}

Como vemos, la leyenda se superpone sobre las barras de la última empresa. Para resolver este problema, situaremos la leyenda en la esquina superior  izquierda. Además, vamos a sustituir en la leyenda los valores de las respuestas por sus significados, y para que quepa, reduciremos el tamaño del texto. 


```r
barplot(Tabla, beside=TRUE, 
        legend.text=c("Muy en desacuerdo", "En desacuerdo","Neutro","De acuerdo","Muy de acuerdo"), 
        main="Diagrama de barras de frecuencias relativas acumuladas\n de respuestas por empresa",
        args.legend=list(x="topleft", cex=0.45))
```



\begin{center}\includegraphics[width=0.9\linewidth]{11chap11_Descripcion_ordinales_files/figure-latex/unnamed-chunk-28-1} \end{center}


<!--
\end{ejemplo}

\begin{figure}[htb]
\begin{center}
\includegraphics[width=0.45\textwidth]{figenc1}\
\includegraphics[width=0.45\textwidth]{figenc2}
\end{center}
\caption{Diagramas de barras  de frecuencias relativas acumuladas de respuestas por empresa en el Ejemplo \@ref(ex:encuestacum).}\label(fig:acumenc)
\end{figure}
-->

\BeginKnitrBlock{example}
<span class="example" id="exm:sprayord"><strong>(\#exm:sprayord) </strong></span>Consideremos el *data frame* `InsectSprays`, que viene predefinido en R. Veamos su estructura.



\EndKnitrBlock{example}


```r
head(InsectSprays)
#>   count spray
#> 1    10     A
#> 2     7     A
#> 3    20     A
#> 4    14     A
#> 5    14     A
#> 6    12     A
str(InsectSprays)
#> 'data.frame':	72 obs. of  2 variables:
#>  $ count: num  10 7 20 14 14 12 10 23 17 20 ...
#>  $ spray: Factor w/ 6 levels "A","B","C","D",..: 1 1 1 1 1 1 1 1 1 1 ...
```
Consultando la Ayuda de `InsectSprays` nos enteramos de que la variable numérica `count` contiene los números de insectos que se encontraron en diferentes superficies agrícolas, todas de la misma área, tratadas con el insecticida indicado por el factor `spray`. 

En primer lugar, vamos a convertir la variable `count` en una variable ordinal que agrupe las entradas de la variable original en los niveles siguientes: "*Entre 0 y 4*", "*Entre 5 y 9*", "*Entre 10 y 14*", "*Entre 15 y 19*" y "*20 o más*". La manera más sencilla de llevarlo a cabo es usando la función `cut`, que estudiaremos en detalle en la  Lección \@ref(chap:cut). Por ahora es suficiente saber que la instrucción


```r
cut(InsectSprays$count, breaks=c(0,5,10,15,20,Inf), right=FALSE,
    labels=c("0-4","5-9","10-14","15-19","20-..."))
```
"cortará" el vector numérico `InsectSprays$count` en intervalos de extremos los puntos especificados en el argumento `breaks`, donde `Inf` indica $\infty$, y el parámetro `right=FALSE` indica que los puntos de corte pertenecen al intervalo a su derecha, formando por lo tanto intervalos cerrados a la izquierda. Así pues, los intervalos en los que esta instrucción clasifica los números de insectos son

$$
[0,5), [5,10), [10,15), [15,20), [20,\infty).
$$
El resultado de la instrucción es un factor no ordenado que tiene como niveles estos intervalos, identificados por medio de las etiquetas especificadas con el parámetro `labels` (es decir, respectivamente, `0-4`, `5-9`, `10-14`, `15-19` y `20-...`) y donde cada entrada de `InsectSprays$count`  ha sido substituida por la etiqueta correspondiente al intervalo al que pertenece. A modo de ejemplo, comparemos las primeras 10 entradas de `InsectSprays$count` con las primeras 10 entradas del resultado de esta función  `cut`:

```r
InsectSprays$count[1:10]
#>  [1] 10  7 20 14 14 12 10 23 17 20
cut(InsectSprays$count, breaks=c(0,5,10,15,20,Inf), right=FALSE,
    labels=c("0-4","5-9","10-14","15-19","20-..."))[1:10]
#>  [1] 10-14  5-9    20-... 10-14  10-14  10-14  10-14  20-... 15-19  20-...
#> Levels: 0-4 5-9 10-14 15-19 20-...
```

Como nosotros vamos a usar estos intervalos como niveles de una variable ordinal, tenemos que convertir el factor resultante en ordenado. Vamos a añadir este factor ordenado como una nueva variable  a una copia de `InsectSprays`.


```r
IS=InsectSprays
IS$count.rank=ordered(cut(IS$count,breaks=c(0,5,10,15,20,Inf),
  right=FALSE, labels=c("0-4","5-9","10-14","15-19","20-...")))
str(IS)
#> 'data.frame':	72 obs. of  3 variables:
#>  $ count     : num  10 7 20 14 14 12 10 23 17 20 ...
#>  $ spray     : Factor w/ 6 levels "A","B","C","D",..: 1 1 1 1 1 1 1 1 1 1 ...
#>  $ count.rank: Ord.factor w/ 5 levels "0-4"<"5-9"<"10-14"<..: 3 2 5 3 3 3 3 5 4 5 ...
head(IS)
#>   count spray count.rank
#> 1    10     A      10-14
#> 2     7     A        5-9
#> 3    20     A     20-...
#> 4    14     A      10-14
#> 5    14     A      10-14
#> 6    12     A      10-14
```
 
Nos interesa estudiar la distribución de los números de insectos según el tipo de insecticida. Por lo tanto, vamos a calcular las tablas bidimensionales de frecuencias relativas y relativas acumuladas de los intervalos de números de insectos en cada nivel de `Spray`, y las representaremos por medio de diagramas de barras. 

La tabla de frecuencias absolutas de los pares (insecticida, intervalo de números de insectos) se puede obtener aplicando `table` al *data frame* formado por las dos últimas columnas de `IS`.


```r
Tab=table(IS[,2:3])
Tab
#>      count.rank
#> spray 0-4 5-9 10-14 15-19 20-...
#>     A   0   1     7     1      3
#>     B   0   1     4     5      2
#>     C  11   1     0     0      0
#>     D   5   6     1     0      0
#>     E   8   4     0     0      0
#>     F   0   1     4     3      4
```
La tabla bidimensional de frecuencias relativas de los intervalos de números de insectos en cada nivel de `Spray` es la siguiente:

```r
Freq.rel=round(prop.table(Tab, margin=1), 3)
Freq.rel
#>      count.rank
#> spray   0-4   5-9 10-14 15-19 20-...
#>     A 0.000 0.083 0.583 0.083  0.250
#>     B 0.000 0.083 0.333 0.417  0.167
#>     C 0.917 0.083 0.000 0.000  0.000
#>     D 0.417 0.500 0.083 0.000  0.000
#>     E 0.667 0.333 0.000 0.000  0.000
#>     F 0.000 0.083 0.333 0.250  0.333
```
y la correspondiente tabla de frecuencias relativas acumuladas (ya traspuesta) es:

```r
Freq.rel.acum=round(apply(prop.table(Tab, margin=1), MARGIN=1, FUN=cumsum), 3)
t(Freq.rel.acum)
#>      count.rank
#> spray   0-4   5-9 10-14 15-19 20-...
#>     A 0.000 0.083 0.667 0.750      1
#>     B 0.000 0.083 0.417 0.833      1
#>     C 0.917 1.000 1.000 1.000      1
#>     D 0.417 0.917 1.000 1.000      1
#>     E 0.667 1.000 1.000 1.000      1
#>     F 0.000 0.083 0.417 0.667      1
```

Los dos diagramas de barras que no interesan son los siguientes:

```r
cyan.col=c("cyan4","cyan3","cyan2","cyan1","cyan") #Colores azulones para las barras
barplot(t(Freq.rel), beside=TRUE, legend=TRUE,  ylim=c(0,1), col=cyan.col, 
  main="Diagrama de barras de frecuencias relativas\n de números de insectos por insecticida")
```



\begin{center}\includegraphics[width=0.9\linewidth]{11chap11_Descripcion_ordinales_files/figure-latex/unnamed-chunk-36-1} \end{center}

```r
barplot(Freq.rel.acum, beside=TRUE, legend=TRUE,col=cyan.col, 
  main="Diagrama de barras de frecuencias relativas acumuladas\n de números de insectos por insecticida", 
  args.legend=list(x="topleft",cex=0.55))
```



\begin{center}\includegraphics[width=0.9\linewidth]{11chap11_Descripcion_ordinales_files/figure-latex/unnamed-chunk-37-1} \end{center}

Observamos que los insecticidas C, D y E son los más efectivos, porque producen mayores números de campos con pocos insectos, mientras que B y F son poco efectivos.

<!--
\begin{figure}[htb]
\begin{center}
\includegraphics[width=0.45\textwidth]{Insect1}\
\includegraphics[width=0.45\textwidth]{Insect2}
\end{center}
\caption{Diagramas de barras de frecuencias relativas y relativas acumuladas de números de insectos por tipo de insecticida en el *data frame* `InsectSprays`.}\label{fig:ISacum}
\end{figure}

\end{ejemplo}
-->

## Guía rápida de funciones

* `ordered` sirve para construir factores ordenados. Sus parámetros principales se pueden consultar en la guía de la Lección \@ref(chap:vect).

* `table` calcula la tabla de frecuencias absolutas de un vector o un factor.

* `t` sirve para trasponer una tabla bidimensional.

* `prop.table` calcula la tabla de frecuencias relativas de un vector o un factor a partir de su tabla de frecuencias absolutas. Sus parámetros principales se pueden consultar en la guía de la Lección \@ref(chap:edqual).

* `cumsum` calcula las sumas acumuladas de un vector.

* `apply(tabla, MARGIN=..., FUN=función)` aplica la `función`  a
los niveles de las variables  de la `tabla`  que se especifican en `MARGIN`. Para calcular frecuencias acumuladas en tablas multidimensionales, se usa `FUN=cumsum`.

* `barplot` dibuja el diagrama de barras de un vector o un factor a partir de una tabla de frecuencias. Sus parámetros principales se pueden consultar en la guía de la Lección \@ref(chap:edqual).

## Ejercicios

### Test {-}

*(1)* Dad una instrucción que defina la tabla de frecuencias absolutas acumuladas de un vector llamado `flores`.

*(2)* Dad una instrucción que defina la tabla de frecuencias relativas acumuladas de un vector llamado `flores` usando la función `prop.table`. 

*(3)* Considerad el vector que forma el fichero [http://bioinfo.uib.es/~recerca/RMOOC/datostest9.txt](http://bioinfo.uib.es/~recerca/RMOOC/datostest9.txt) como una variable ordinal de niveles 1, 2, 3, ... , 9, ordenados con su orden creciente natural. ¿Cuál es la frecuencia relativa acumulada de 6 en esta variable, redondeada a 3 cifras decimales? Dad su valor, no cómo lo habeis calculado.

*(4)* Considerad la tabla de datos del *url* [http://bioinfo.uib.es/~recerca/RMOOC/Felizdata.txt](http://bioinfo.uib.es/~recerca/RMOOC/Felizdata.txt). Considerad su variable `nivel.feliz` como una variable ordinal con niveles ordenados   `Infeliz` <  `Poco.feliz` <  `Feliz`  < `Muy.Feliz`. ¿Cuál es la frecuencia relativa acumulada del nivel `Feliz` entre los estudiantes de 2^o^ curso, redondeada a 3 cifras decimales?  Dad su valor, no cómo lo habeis calculado.




### Ejercicio {-}

La tabla de datos que encontraréis en el *url*  [http://aprender.uib.es/Rdir/Notas2011A.txt](http://aprender.uib.es/Rdir/Notas2011A.txt)  contiene las notas obtenidas por los estudiantes de los grados de Biología y Bioquímica de la UIB en un examen de la asignatura Matemáticas I  del curso 2011-12 (no aparecen los no presentados, por lo que no hay valores `NA`). Las variables que contiene la tabla para cada estudiante son: su nota numérica (sobre 10), su calificación alfabética (S  significa Suspenso, A, Aprobado, N  Notable, y E, Sobresaliente) y su grupo (BLM para el grupo de las mañanas de Biología, BLT  para el grupo de las tardes de Biología y BQ  para Bioquímica). 


*(a)* Definid un *data frame* con esta tabla, de manera que su variable `NotasLetra` sea un factor ordenado, con las calificaciones alfabéticas ordenadas según su orden natural S < A < N < E. Comprobad con `str` y `head` que el *data frame* obtenido tiene la estructura deseada.

*(b)* Comprobad que las notas alfabéticas se corresponden con las notas numéricas: [0,5) corresponde a S; [5,7), a A; [7,9), a N; y  [9,10], a E. Si hay algún error, corregid la nota alfabética.

*(c)* Calculad la tabla bidimensional de frecuencias relativas de las calificaciones alfabéticas por grupo, con las frecuencias relativas calculadas dentro de los grupos. Redondead las frecuencias a 2 cifras decimales. Los grupos tienen que definir las filas, y las notas, las columnas.

*(d)* Calculad la tabla bidimensional de frecuencias relativas acumuladas de las calificaciones alfabéticas por grupo, con las frecuencias relativas calculadas dentro de los grupos. Redondead a 2 cifras decimales. Los grupos tienen que definir las filas, y las notas, las columnas.

*(e)* Dibujad un diagrama de barras por bloques de las frecuencias relativas
 de las calificaciones alfabéticas dentro de cada grupo: los bloques han de corresponder a los grupos. Poned un título al gráfico y añadid una leyenda que explique cada barra qué calificación representa. Podéis poner colores, cambiar los nombres, etc.  para mejorar su aspecto.

*(f)* Dibujad un diagrama de barras por bloques de las frecuencias relativas acumuladas de las calificaciones alfabéticas dentro de cada grupo: los bloques han de corresponder a los grupos. Como antes, poned un  título al gráfico y añadid una leyenda que explique cada barra qué calificación representa. Podéis poner colores, cambiar los nombres, etc.  para mejorar su aspecto.

*(g)* ¿Podéis extraer alguna conclusión de las tablas y los gráficos anteriores?


### Respuestas al test {-}




*(1)* `cumsum(table(flors))`

*(2)* `cumsum(prop.table(table(flors)))`

*(3)* 0.397

*(4)* 0.763

