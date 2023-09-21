#   Predicción de Calidad en Planta de Flotación Minera - Proyecto Académico con Enfoque de Aprendizaje Supervisado 

## Contexto del Proceso de Flotación

![](https://github.com/UrsulaMoya/mi-primer-repositorio-para-la-minera/blob/main/columna%20flotacion%20limpia.jpg)

El proceso de flotación es un procedimiento de extracción de metal (hierro) a partir de su mineral. Se concentra el metal hasta que su ley sea adecuada (mínimo 60% de hierro) para uso en procesos metalúrgicos (hierro metálico y acero). Durante este proceso, en cada columna se trituran los minerales antes de mezclarlos con agua para convertirlos en pulpa; la superficie de esta pulpa es selectivamente convertida para repeler el agua a través del uso de reactivos específicos (amina, almidón). Luego los minerales de la pulpa se separan a través de un flujo de burbujas de aire que se adhieren a las partículas que repelen el agua para que floten y así son recolectadas en una espuma (partículas de sílica). Se espera que el contenido de la sílica al final del procesos se encuentre entre un rango ideal (entre  $0,5$% y 2%) para asegurar la calidad del concentrado de hierro.

## Descripción detallada del proyecto, propósito y contexto

Se cuenta con información entregada correspondiente a datos tabulados en un archivo de tipo csv. El conjunto de datos proviene de una planta de flotación con 737.453 observaciones ordenadas
y antiguas, entre marzo y septiembre de 2017. La dimensión de los datos es 24: reportando 23 variables simples cuantitativas de tipo flotante (continuas) y 1 variable fecha compuesta (discreta) inicialmente detectada como de tipo object por Pandas. En total hay 4097 instancias distintas de horas con alrededor de 174 a 180 muestras. En relación a la flotación se toman medidas antes de la planta de flotación, en el proceso de flotación y al final del proceso, y el objetivo es: a partir de los datos predecir el porcentaje de concentrado de sílica en el proceso (medido al final en el laboratorio). Se asume que la variable a predecir es de tipo estática y las potenciales variables explicativas son: 
                
1. Alimentación de hierro
2. Alimentación de sílica
3. Flujo de amina
4. Flujo de pulpa mineral
5. pH de pulpa mineral
6. Densidad de la pulpa de mineral
7. Flujo de aire en cada una de las 7 columnas de flotación
8. Nivel en cada una de las 7 columnas de flotación
9. Concentrado de hierro.

No hay datos faltantes, ni valores fuera de rango de los atributos. Se excluyen los duplicados del an´alisis quedando un conjunto de 736.282 datos. En el análisis se efectúa un estudio de potenciales outliers con diversas estrategias de remoción. Se considera un dato atípico a aquel que, en general, se encuentran fuera del intervalo [Q1 − 1, 5 ∗ RIQ, Q3 + 1, 5 ∗ RIQ], donde Q1 y Q3 corresponden al primer y tercer cuartil respectivamente, RIQ = Q3−Q1 es el rango intercuartílico (largo de la caja en el boxplot). Se muestra un método de remoción de datos atípicos para contrastar los modelos a evaluar. Este método aplica la función stats.iqr de la librería scipy que ejecuta horizontalmente la eliminación (se obtiene la detección de 203.029 potenciales outliers correspondiente al 27.57 % de los datos con la exclusión de las filas duplicadas).

Se presenta un breve análisis exploratorio indagando medidas de centralidad y de extensión. Se exhibe un análisis para entender y modelar cómo el porcentaje de sílica se ve afectado por los otros factores del proceso de flotación, el cual es realizado para disminuir la concentración de sílica presente en el mineral de hierro. Este análisis considera una descripción de los datos de tipo general, relaciones y comparaciones pertinentes tipo scatter plot, boxplot y correlaciones lineales. Esto en virtud de poder entrever alguna hipótesis para el objetivo planteado de predecir el porcentaje de concentración final de sílica. Se hace un estudio habitual de posibles outliers a través de boxplot exponiendo el análisis exploratorio de forma comparativa con y sin potenciales outliers. El estudio es efectuado en virtud de lo aprendido en un curso de Fundamentos de Ciencia de Datos. 

Se buscó una relación lineal en los parámetros, construyendo un modelo predictivo de la variables Y del concentrado de sílica a partir de las variables $X_1, X_2, ..., X_{22}$ de modo que 

$$Y=  \beta_ 0 +\sum_{j=1}^{22} \beta_ j g(X_{j}) + \epsilon = \beta_ 0 + \beta_ 1 g(X_{1}) +\beta_ 2 g(X_{2})+\cdot+\beta_{22} g(X_{22})+ \epsilon ,$$
donde  $g$  es una función no necesariamente lineal en la variable $X_{j}$ y $\epsilon$ corresponde al error aleatorio.

Se contrarrestaron diversos ajustes de modelos lineales para distintos conjuntos de datos, pasando por modelos polinomiales en las variables predictoras y se aplicó reducción de la dimensionalidad a un conjunto de datos sin duplicados, sin outliers, sin variables correlacionadas fuertemente y transformando según PCA. Se utilizó validación cruzada con 70% de datos para entrenar y 30% para testear. 



## Tecnologías Utilizadas

Los análisis expuestos hacen uso de las librerías pandas, numpy, datatime, matplotlib, seaborn, scipy y sklearn en lenguaje de programación Python
con Notebook de Jupyter. 

## Instalación

[Instrucciones claras sobre cómo instalar y configurar el proyecto localmente, incluyendo las dependencias si es necesario]

## Uso

[Instrucciones sobre cómo utilizar el proyecto, incluyendo ejemplos y comandos si aplican]

## Resultados

En el histograma  de la distribución de los valores del porcentaje concentrado de sílica se observó un valor máximo de frecuencia significativamente menor que en el análisis  del concentrado de sílica con outliers. La desviación estándar disminuyó ligeramente. Los valores de los percentiles disminuyeron respecto a los datos que incluían outliers. La forma general de la distribución se mantuvo, al igual que las distancia de la media a los percentiles. En el boxplot de la distribución de los valores sin outliers del porcentaje de sílica mediante laboratorio, se observó que a pesar de que el sesgo hacia la derecha (sesgo positivo) permaneció, se visualiza que el centro de la caja se desplazó levemente hacia la izquierda del 2% que es el máximo ideal. 

![](https://github.com/UrsulaMoya/mi-primer-repositorio-academico-minero/blob/main/histograma42.png)

Con o sin datos atípicos, los valores del flujo de aire en el proceso de flotación de las columnas presentaron mayor dispersión y asimetrías moderadas en las columnas 1,2,3,6 y 7. En las columnas 4 y 5 se presentaron rangos pequeños y menor dispersión.

![](https://github.com/UrsulaMoya/mi-primer-repositorio-academico-minero/blob/main/caja6.png)


Se presentaron correlaciones lineales altas entre la alimentación de hierro y sílica, también entre las columnas 1 y 2, y entre los flujos en columnas 1 y 3, entre los flujos de columnas 2 y 3, y entre las columnas 6 y 7.

![](https://github.com/UrsulaMoya/mi-primer-repositorio-academico-minero/blob/main/correlaciones3.png)

Al aplicar PCA en un conjunto reducido se redujo de 17 a 8 atributos, obteniéndose finalmente las siguientes métricas en los modelos de Machine Learning

![](https://github.com/UrsulaMoya/mi-primer-repositorio-academico-minero/blob/main/resultados.png)

Para predecir la sílica final en el proceso de flotación minera se escoge el modelo de regresión lineal entrenado en el conjunto $C_1,$$ pues el indicador MSE no es alto y el coeficiente de determinación $$R^2$$ es el más alto.

## Aprendizajes

El orden del procedimiento empleado en este proyecto podría cambiar los rendimientos de los modelos.

## Contribución

[Cualquier comentario es bien recibido, idealmente por correo de perfil.]

## Licencia

[Indica la licencia bajo la cual se publica el proyecto]

---

[Opcional: Agrega cualquier información adicional, enlaces a recursos externos o créditos]

[Incluye una sección de contacto si deseas que las personas se pongan en contacto contigo para obtener más información]

