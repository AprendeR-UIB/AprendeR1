# Distribuciones de probabilidad {#chap:distr}

R conoce los tipos de distribución de probabilidad más importantes, incluyendo las que mostramos en la  tabla siguiente: 







$$
\begin{array}{lll}
\hline
\textbf{Distribución} & {\textbf{Nombre en R}} & {\textbf{Parámetros}}\\ \hline
\mbox{Binomial} &{\texttt{binom}} & \mbox{tamaño de la muestra $n$, probabilidad $p$}\\
\mbox{Geométrica} & {\texttt{geom}} & \mbox{$p$}\\
\mbox{Hipergeométrica} & {\texttt{hyper}} & \mbox{tamaño de la población $N$, número poblacional}\\[-0.75ex] 
& & \mbox{de éxitos $M$, tamaño de la muestra $n$}\\
\mbox{Poisson} & {\texttt{pois}} & \mbox{esperanza $\lambda$}\\
\mbox{Uniforme} & {\texttt{unif}} & \mbox{mínimo, máximo}\\
\mbox{Exponencial} & {\texttt{exp}} & \lambda\\
\mbox{Normal} & {\texttt{norm}} & \mbox{media $\mu$, desviación típica $\sigma$}\\
\mbox{Khi cuadrado} & {\texttt{chisq}} & \mbox{número de grados de libertad $df$}\\
\mbox{t de Student} & {\texttt{t}} & \mbox{número de grados de libertad $df$}\\
\mbox{F de Fisher} & {\texttt{f}} & \mbox{los dos números de  grados de libertad}
\\ \hline
\end{array}
$$

Para cada una de estas distribuciones, R sabe calcular cuatro funciones, que se obtienen añadiendo un prefijo al nombre de la distribución: 

* La función de densidad, con el prefijo **d**.

* La función de distribución de probabilidad, con el prefijo **p**; esta función dispone además del parámetro `lower.tail` que igualado a `FALSE` calcula la **función de distribución de cola superior**: la probabilidad de que una variable aleatoria con esta distribución de probabilidad tome un valor estrictamente mayor que uno dado.

* Los cuantiles, con el prefijo **q**.

* Vectores de números aleatorios con esta distribución, con el prefijo **r**.

La función correspondiente se aplica entonces al valor sobre el que queremos calcular la función y a los parámetros de la distribución (en este orden, y los parámetros en el orden en que los damos en la tabla anterior, cuando hay más de uno).

Por ejemplo, sea $X$ una variable aleatoria binomial $B(20,0.3)$, es decir,  de tamaño $n=20$ y probabilidad $p=0.3$,  y sean $f_X$ su función de densidad y $F_X$ su función de distribución. Calculemos algunos valores de funciones asociadas a esta variable aleatoria.

* $f_X(5)=P(X=5)$:


```r
dbinom(5,20,0.3)
#> [1] 0.1788631
```

|        Comprobémoslo, recordando que si $X\sim B(n,k)$, entonces $P(X=k)=\binom{n}{k}p^k(1-p)^{n-k}$:


```r
choose(20,5)*0.3^5*0.7^15
#> [1] 0.1788631
```



* $f_X(8)=P(X=8)$:


```r
dbinom(8,20,0.3)  
#> [1] 0.1143967
```

* $F_X(5)=P(X\leq 5)$:

```r
pbinom(5,20,0.3)  
#> [1] 0.4163708
```

|        Comprobémoslo, usando que $P(X\leq 5)=\sum_{k=0}^5 P(X=k)$:


```r
sum(dbinom(0:5,20,0.3))
#> [1] 0.4163708
```


* $F_X(8)=P(X\leq 8)$:


```r
pbinom(8,20,0.3)  
#> [1] 0.8866685
```

* $P(X>8)$


```r
pbinom(8,20,0.3,lower.tail=FALSE)
#> [1] 0.1133315
```

|        En efecto:


```r

1-pbinom(8,20,0.3)
#> [1] 0.1133315
```



* El cuantil de orden $0.5$ de $X$, o sea, su **mediana**: el valor $x$ más pequeño tal que $P(X\leq x)\geq 0.5$


```r
qbinom(0.5,20,0.3)  
#> [1] 6
```

|        Comprobemos que $P(X\leq 6)\geq 0.5$ y en cambio $P(X\leq 5)< 0.5$:


```r
pbinom(6,20,0.3) 
#> [1] 0.6080098
pbinom(5,20,0.3) 
#> [1] 0.4163708
```


* El cuantil de orden $0.25$ de $X$, es decir, su **primer cuartil**:



```r
qbinom(0.25,20,0.3)  
#> [1] 5
```

* Un vector aleatorio de 10 valores generado con la variable aleatoria $X$:


```r
rbinom(10,20,0.3)
#>  [1]  7  4  7 10  7  7  6  6  8  3
```

* Dos vectores aleatorios más, de 10 valores cada uno, generados con la variable aleatoria $X$:



```r
rbinom(10,20,0.3) 
#>  [1] 7 7 1 7 5 6 7 6 7 5
rbinom(10,20,0.3)
#>  [1] 7 8 5 5 7 7 8 7 4 8
```



Del mismo modo, si estamos trabajando con una variable aleatoria $Y$ de Poisson con parámetro $\lambda=5$:


* $P(Y=8)$:


```r
dpois(8,5) 
#> [1] 0.06527804
```


* $P(Y\leq 8)$:


```r
ppois(8,5) 
#> [1] 0.9319064
```

* El cuantil de orden 0.6 de $Y$:


```r
qpois(0.6,5)
#> [1] 5
```

* Un vector aleatorio de 20 valores generado con la variable aleatoria $Y$:


```r
rpois(20,5)
#>  [1]  1  2  3  6  5  2 10  3  7  4  3  3  7  5  7  4  4  4  5  4
```


Si no entramos ningún parámetro en las funciones asociadas a la distribución normal, R entiende que se trata de la normal estándar (con media $\mu=0$ y desviación típica $\sigma=1$): por ejemplo, las dos instrucciones siguientes nos dan el valor $f_Z(0.3)$ de la función densidad de una normal estándar $Z$ aplicada a 0.3 (que *no* es igual a $P(Z=0.3)$):


```r
dnorm(0.3)
#> [1] 0.3813878
dnorm(0.3,0,1)
#> [1] 0.3813878
```

Las funciones densidad y distribución de una variable aleatoria se pueden dibujar con la función `curve`. Así, la función siguiente dibuja la gráfica de la densidad de una variable normal estándar de la Figura \@ref(fig:dnorm):


```r
curve(dnorm(x,0,1.5),-5,5,xlab="",ylab="",main="")
```

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{09chap08_Distribuciones_files/figure-latex/dnorm-1} 

}

\caption{Función densidad de una variable *N*(0,1).}(\#fig:dnorm)
\end{figure}

De manera similar, la función siguiente dibuja la gráfica de la función de distribución de una variable normal estándar de la Figura \@ref(fig:pnorm):


```r
curve(pnorm(x,0,1.5),-5,5,xlab="",ylab="",main="")
```

\begin{figure}

{\centering \includegraphics[width=0.9\linewidth]{09chap08_Distribuciones_files/figure-latex/pnorm-1} 

}

\caption{Función distribución de una variable *N*(0,1).}(\#fig:pnorm)
\end{figure}

## Ejercicios


### Test {-}

*(1)* Sea $f$ la función de densidad de una variable aleatoria normal con $\mu=0.2$ y $\sigma=1.2$. Dad el valor de $f(0.5)$ redondeado a 4 cifras decimales. 

*(2)* Sea $X$ una variable aleatoria normal con $\mu=0.2$ y $\sigma=1.2$. Dad el valor de $P(3\leq X\leq 7)$ redondeado a 4 cifras decimales. 

*(3)* Sea $X$ una variable aleatoria $B(10,0.2)$. Dad el valor de $P(3\leq X\leq 7)$ redondeado a 4 cifras decimales. 

*(4)* Dad una instrucción que calcule la mediana de una lista de 20 números aleatorios generados con distribución $B(10,0.2)$. No deis el resultado, solo la instrucción.


### Problemas {-}

**(1)** Según [la página web de *Tall.Life*](https://tall.life/height-percentile-calculator-age-country/), la altura de los hombres españoles adultos sigue una distribución aproximadamente normal de media 173.1 cm y desviación típica 7.42 cm, mientras que la de las mujeres españolas adultas sigue una distribución también aproximadamente normal, pero de media 160.3 cm y desviación típica 7.11 cm.
Por otro lado, según [el último *FactBook* sobre España de la CIA](https://www.cia.gov/library/publications/the-world-factbook/geos/sp.html), aproximadamente un 51% de los españoles adultos son mujeres. Vamos a tomar todos estos datos como exactos y verdaderos. 

*(a)* ¿Qué es más probable, que un hombre adulto español sea más alto que Víctor Claver (2.05 m) o que una mujer adulta española sea más alta que Alba Torrens (1.90 m)?

*(b)* Si tomamos un español adulto (hombre o mujer) al azar, ¿qué es más probable, que sea más alto que Marc Gasol (2.11 m) o que sea más bajo que Peter Dinklage (1.35m)?

**(2)** He lanzado un dado de 6 caras 100 veces, y he obtenido 24 veces un 6.  Suponed que el dado es honrado. Considerad la variable aleatoria $X$ dada por el número de veces que obtenemos un 6 al lanzar el dado 100 veces al aire.

*(a)* ¿Qué distribución de probabilidad tiene $X$? Tenéis que dar el tipo de distribución y sus parámetros.

*(b)* ¿Qué vale $P(X=24)$? Es decir, ¿cuál es la probabilidad de sacar exactamente 24 seises en 100 lanzamientos del dado?

*(c)* ¿Cuál es la probabilidad de sacar 24 seises o más en 100 lanzamientos del dado?

*(d)* Simulad con R una secuencia aleatoria de 1000 realizaciones de $X$: es decir, generad un vector de 1000 números aleatorios con la distribución de probabilidades de $X$. Vamos a suponer que este vector nos da los números de seises obtenidos en 1000 secuencias de 100 lanzamientos del dado cada una. ¿En qué porcentaje de estas secuencias habéis obtenido exactamente 24 seises?  ¿En qué porcentaje habéis obtenido al menos 24 seises? ¿Son consistentes estos resultados con los valores obtenidos en *(b)* y *(c)*?


<!--**(1)** Como sabéis, si $X$ es una variable aleatoria Bernoulli $Be(p)$, es decir, de probabilidad de éxito $p$, e $Y$ es la variable aleatoria que nos da el número de fracasos antes de obtener el primer éxito en una secuencia de repeticiones independientes de $X$, entonce $Y$ sigue una  **distribución geométrica** $Ge(p)$.  

Por lo tanto, si efectuamos una serie de lanzamientos independientes de una moneda no trucada, las longitudes de las **rachas de cruces** (las secuencias de cruces entre pares de caras consecutivas) que nos salgan seguirán una distribución geométrica $Ge(0.5)$, porque nos dan los números de cruces (fracasos) obtenidos antes de sacar una cara (éxito) en repeticiones independientes de una v.a. $Be(0.5)$, reiniciando el contador en cada cara. Vamos a comprobarlo a mediante una simulación sencilla. 

*(a)* Generad un vector aleatorio binario $X$ de longitud 10^6^ con distribución Bernoulli $Be(0.5)$, que representará un millón de lanzamientos de una moneda honrada (0 cruz, 1 cara). Quedaos con el vector que va de su primer 1 a su último 1, y seguid llamándole $X$ al vector resultante.

*(b)* Calculad las longitudes de todas las secuencias maximales de 0s en $X$ (es decir, de las secuencias de 0s que separan pares de 1s consecutivos). Por lo que hemos explicado, estas longitudes deberían seguir una distribución geométrica $Ge(0.5)$.

*(c)* Dibujad un histograma de líneas de las frecuencias relativas de las longitudes de cadenas maximales de ceros obtenidas de esta manera, y superponed un diagrama poligonal de las probabilidades de dichas longitudes según la distribución $Ge(0.5)$. Para mejorar la visibilidad del gráfico, representad solo las longitudes $k$ cuya probabilidad bajo una distribución $Ge(0.5)$ sea al menos  0.0001. Comentad el gráfico obtenido.
-->

### Respuestas al test {-}

*(1)* 0.3222

Nosotros lo hemos calculado con 

```r
round(dnorm(0.5,0.2,1.2),4)
#> [1] 0.3222
```

*(2)* 0.0098

Nosotros lo hemos calculado con 

```r
round(pnorm(7,0.2,1.2)-pnorm(3,0.2,1.2),4)
#> [1] 0.0098
```


*(3)* 0.3221

Nosotros lo hemos calculado con 

```r
round(pbinom(7,10,0.2)-pbinom(2,10,0.2),4)
#> [1] 0.3221
```
También se obtiene el resultado correcto con 

```r
round(sum(dbinom(3:7,10,0.2)),4)
#> [1] 0.3221
```
En cambio, con  

```r
round(pbinom(7,10,0.2)-pbinom(3,10,0.2),4)
#> [1] 0.1208
```
no se obtiene el resultado correcto. Pensad por qué aquí hay que restar `pbinom(2,10,0.2)` y en la pregunta anterior restábamos `pnorm(3,0.2,1.2)`.

*(4)* `median(rbinom(20,10,0.2))`

También sería correcto `median(rbinom(20,size=10,prob=0.2))`, pero no es necesario dar los nombres de los parámetros si entráis sus valores en el orden correcto, y por eso no los hemos explicado.


### Soluciones sucintas de los problemas  {-}



**(1)** *(a)* La probabilidad que un hombre adulto español sea más alto que Víctor Claver es

```r
pnorm(205,173.1,7.42,lower.tail=FALSE)
#> [1] 0.00000857112
```
y la probabilidad de que una mujer adulta española sea más alta que Alba Torrens es

```r
pnorm(190,160.3,7.11,lower.tail=FALSE)
#> [1] 0.00001475499
```

*(b)* La probabilidad de que un español adulto sea más alto (o alta) que Marc Gasol es

```r
0.49*pnorm(211,173.1,7.42,lower.tail=FALSE)+0.51*pnorm(211,160.3,7.11,lower.tail=FALSE)
#> [1] 0.00000007984638
```
y la probabilidad de que un español adulto sea más bajo (o baja) que Peter Dinklage es

```r
0.49*pnorm(135,173.1,7.42)+0.51*pnorm(135,160.3,7.11)
#> [1] 0.00009522642
```


**(2)**  *(a)* Binomial $B(100,1/6)$

*(b)* `dbinom(24,100,1/6)`=0.016161

*(c)* `1-pbinom(23,100,1/6)`=0.0378644

*(d)* El vector siguiente contiene una simulación como la pedida

```r
Simulación=rbinom(1000,100,1/6)
```

En este vector, el porcentaje de entradas iguales a 24 es

```r
round(100*length(Simulación[Simulación==24])/1000,1)
#> [1] 1.9
```

y el porcentaje de entradas mayores o iguales a 24 es

```r
round(100*length(Simulación[Simulación>=24])/1000,1)
#> [1] 3.8
```
Naturalmente, en cada simulación puede dar valores diferentes. Por ejemplo, si repetimos de nuevo la simulación

```r
Simulación2=rbinom(1000,100,1/6)
```
obtenemos:

```r
round(100*length(Simulación2[Simulación2==24])/1000,1)
#> [1] 2
round(100*length(Simulación2[Simulación2>=24])/1000,1)
#> [1] 3.3
```




<!--
**(1)** *(a)* Como la distribución $Be(p)$ es la distribución binomial $B(1,p)$, podemos construir $X$ por medio de: 

```r
X=rbinom(10^6,1,0.5)
X=X[min(which(X==1)):max(which(X==1))]
```

*(b)* Las longitudes de cadenas maximales de 0s en $X$ serán las diferencias entre posiciones consecutivas de 1s en $X$, menos 1 (si, digamos, hay un 1 en la posición 5a y el siguiente 1 está en la posición 13a, en medio hay $13-5-1=7$ 0s). Por lo tanto, el vector $Y$ de longitudes de cadenas maximales de 0s en $X$ se puede calcular con:

```r
Exitos=which(X==1)
Y=diff(Exitos)-1
```

*(c)* Calculemos el mayor número natural $M$ tal que si $Y$ es una v.a. $Ge(0.5)$, $P(Y=M)\geq 10^{-4}$:

```r
M=max(which(dgeom(0:100,0.5)>=10^(-4)))-1
M
#> [1] 12
```

El gráfico pedido es entonces:

```r
n=0:M
plot(prop.table(table(Y)[n]),col="blue",type="h",xlab="Longitudes de cadenas maximales de 0s",ylab="Probabilidades")
points(n,dgeom(n,0.5),col="red",type="o",pch=20,cex=0.5)
```



\begin{center}\includegraphics[width=0.9\linewidth]{09chap08_Distribuciones_files/figure-latex/unnamed-chunk-39-1} \end{center}
-->
