# SolucionesTema1
---
title: "Boletín Tema 1"
subtitle: Tratamiento de Datos. Grado en Ciencia de Datos- UV
author: "Marcelino Martínez"
date:  "`r Sys.Date(15/02/2023)`"  
params:
  lang: ES
lang: "`r switch(params$lang, ES = 'es-ES', EN = 'en-US')`"
output:
  pdf_document:
    toc: no
    toc_depth: 3
    number_sections: yes
  html_notebook:
    echo: yes
    number_sections: yes
    toc: yes
  html_document:
    echo: yes
    number_sections: yes
    theme: lumen
    toc: yes
language:
  label:
    fig: 'Figura '
    tab: 'Tabla '
    eq: 'Ecuación '
    thm: 'Teorema '
    lem: 'Lema '
    def: 'Definición '
    cor: 'Corolario '
    prp: 'Proposición '
    exm: 'Ejemplo '
    exr: 'Ejercicio '
    proof: 'Demostración. '
    remark: 'Nota: '
    solution: 'Solución. '
---

```{r setup, cache = F, echo = F, message = F, warning = F, tidy = F,}
# CONFIGURACIÓN GENERAL
library(knitr)
options(width = 100)
# Opciones generales chunks
## PARA GENERAR SOLO LOS ENUNCIADO include=FALSE
#opts_chunk$set(echo=F,message = F, error = F, warning = F, comment = NA, fig.align = 'center', dpi = 100, tidy = F, cache.path = '.cache/', fig.path = './figure/', include=FALSE)
## PARA Incluir la soluciones SOLO LOS ENUNCIADO include=TRUE
opts_chunk$set(echo=T,message = F, error = F, warning = F, comment = NA, fig.align = 'center', dpi = 100, tidy = F, cache.path = '.cache/', fig.path = './figure/', include=TRUE)
#options(xtable.type = 'html')
knit_hooks$set(inline = function(x) {
  
  if(is.numeric(x)) {
    round(x, getOption('digits'))
  } else {
    paste(as.character(x), collapse = ', ')
  }
})
#knit_hooks$set(plot = knitr:::hook_plot_html)
```

```{r,echo=FALSE}
# Especificamos las librerías necesarias en esta lista
packages = c("MASS","knitr","tidyverse","robustbase","car")
#use this function to check if each package is on the local machine
#if a package is installed, it will be loaded
#if any are not, the missing package(s) will be installed and loaded
package.check <- lapply(packages, FUN = function(x) {
  if (!require(x, character.only = TRUE)) {
    install.packages(x, dependencies = TRUE)
    library(x, character.only = TRUE)
  }
})
#verify they are loaded
#search()
```

1.  Considera los conjuntos de datos **mammals** del paquete **MASS** y **Animals2** del paquete **robustbase**.

<!-- -->

a.  Mira la las características de ambos conjuntos usando la ayuda.
b.  Usa las funciones **dim, head, tail, str** para una primera visión de los conjuntos de datos.
c.  Muestra los nombres de las filas y las columnas (**rownames**, **colnames**)

```{r}
dim(mammals)
head(mammals)
tail(mammals)
str(mammals)
```
```{r}
rownames(mammals)
colnames(mammals)
```

d.  Usa la función **intersect** y almacena en la variable *commonAnimals* los aminales que aparezcan en ambos conjuntos

```{r}
x <- rownames(mammals)
y <- colnames(mammals)
commonAnimals <- intersect(x,y)
```

e.  Usa **setdiff** para averiguar qué animales no están en ambos conjuntos. ¿Cuántos son ?. ¿Qué tipo de animales son?

```{r}
setdiff(x,y)
```

e.  Determina las diferencia entre los animales que no aparecen en ambos conjuntos.

```{r}
```

2.  La funcion **qqPlot** del paquete **car** puede ser utilizada para determinar gráficamente si una serie de puntos siguen una distribución de datos Gaussiana. Si las muestras están dentro de las líneas discontinuas podemos indicar que siguen una distribución Gaussiana con un 95 % de confianza. Utilizando esta función representa el logaritmo neperiano (**log**) del peso del cerebro (**brain weigths**) del registro de datos **mammals** del paquete **MASS** y conjunto de datos **Animals2** de la librería **robustbase**. ¿Presentan el mismo comportamiento ?.¿Podríamos decir que siguen una distribución Gaussiana ?

```{r}
qqPlot(log(mammals$brain))
#Vemos como las muestras están dentro de las líneas discontinuas, por lo que podemos indicar que siguen una distribución Gaussiana con un 95 % de confianza.
```

3.  La función **library** sin argumentos abre una ventana y muestra las librerías que han sido instaladas.

    a.  Asigna el valor devuelto por esta función a la variable **libReturn** y observa su estructura.
    b.  Uno de los elementos de la lista es un matriz de caracteres. Muestra por pantalla los 5 primeros elementos de esta matriz usando la función **head**.
    c.  Determina el número de librerías que tienes instaladas.

```{r}
libReturn <- library()
head(libReturn)
#Podemos observar que el número de librerías instaladas es de 179.
```

4.  En las transparencias del tema 1 se citan los primeros pasos a seguir cuando se analiza un nuevo conjunto de datos.

    a.  Determina las tres primeras etapas para el conjunto de datos **cabbages** del paquete **MASS**
    b.  Puedes determinar el número de valores perdidos (almacenados como **NA** en R) usando la función **is.na**. Determina el número de valores perdidos para cada una de las variables del conjunto **cabbages**.
    c.  Repite los apartados anteriores con el conjunto de datos **Chile** del paquete **car**.
    d.  Utiliza la función **summary**, sobre **cabbages** y **Chile** y observa como, además de otros estadísticos, también devuelve el número de valores perdidos de cada variable.

```{r}
is.na(cabbages)
sum(is.na(cabbages))
#No hay ningun NA en el conjunto de datos

is.na(Chile)
sum(is.na(Chile))
#En cambio, en este conjunto de datos si que observamos que hay NA, en concreto hay 295

summary(cabbages)
summary(Chile)
```



5.  Muchas pruebas estadísticas suponen que los datos siguen una distribución Gaussiana. Utiliza la aproximación visual proporcionada por **qqPlot** para determinar si podemos asumir que las variables **HeadWt** y **VitC** del conjunto **cabbages** verifican esta condición.

```{r}
qqPlot(cabbages$HeadWt)
qqPlot(cabbages$VitC)
##Vemos como en los dos casos las muestras están dentro de las líneas discontinuas, por lo que podemos indicar que siguen una distribución Gaussiana con un 95 % de confianza.
```

6.  Una representación habitual, para determinar la distribución de los datos de una variable cuantitativa es el histograma (**hist**). Determina, de forma aproximada, utilizando el histograma, si hay diferencias entre los contenidos de vitamina C (**VitC**), para las diferentes variedades de calabaza (variable **Cult**), en el conjunto de datos **cabbages**.

```{r}
hist(cabbages$VitC)
#hist(cabbages$Cult)
#No podemos representar las diferentes variedades de calabaza ya que no es numérico
```

7.  Un modelo sencillo para relacionar variables es la *predicción lineal*. En el siguiente ejemplo se utiliza el conjunto de datos **whiteside**, de la librería **MASS**. Esta aproximación propone un modelo que predice una variable a partir de otra. Una primera etapa para plantear esta aproximación sería representar ambas variables mediante un diagrama de dispersión (Gráfico XY) y determinar si la relación entre variables "parece" lineal. Si es así, podemos plantear un modelo lineal (en este caso según un factor), donde se aprecia claramente que existe una relación lineal entre las dos variables consideradas. Observa y ejecuta el siguiente código.

```{r, echo=T,eval=F}
#Diagrama de dispersión global.
plot(whiteside$Temp, whiteside$Gas)
#Diagrama de dispersión etiquetando según un factor.
plot(whiteside$Temp, whiteside$Gas, pch=c(6,16)[whiteside\$Insul])
legend(x="topright",legend=c("Insul = Before","Insul = After"), pch=c(6,16))
# Planteamos 2 modelos lineales, uno para los datos de cada factor
Model1 <- lm(Gas ~ Temp, data = whiteside, subset = which(Insul == "Before"))
Model2 <- lm(Gas ~ Temp, data = whiteside, subset = which(Insul == "After"))
# Representamos las rectas correspondientes a cada modelo lineal
abline(Model1, lty=2)
abline(Model2)
```



a.  Utiliza un procedimiento análogo para determinar si se aprecia una relación lineal entre los niveles de vitamina C, **VitC** en función del peso de la calabaza, **HeadWt**, en el conjunto de datos **cabbages**.

```{r,echo=T,include=T,eval=F}
plot(cabbages$VitC, cabbages$HeadWt)
```

b.  Repite el apartado anterior, pero obteniendo un modelo para cada una de las dos variedades de calabaza, **Cult**. Ver[Parámetros básicos plot](https://www.statmethods.net/advgraphs/parameters.html).

```{r}
plot(cabbages$Cult)
```

c.  Usa **summary** con cada uno de los modelos obtenidos y observa **Coefficients**. Dado que hemos planteado un modelo $y=mx+n$, donde $y=VitC$ y $x=HeadWt$. La función **lm** nos permite obtener **(Intercept)**; **n** y la pendiente **HeadWt**; **m** (además de otros parámetros adicionales que evalúan la caracterísiticas del modelo). Observa que en todos los casos, la pendiene es negativa indicando que las calabazas de más peso contienen menos vitamina C. No te preocupes por el resto de parámetros del modelo, por el momento.

```{r}
summary(cabbages$VitC, cabbages$HeadWt)
summary(cabbages$Cult)

```
