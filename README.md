# Predicción de Calidad en Planta de Flotación Minera (Proyecto Académico) 

## Contexto del Proceso de Flotación

![](https://github.com/UrsulaMoya/mi-primer-repositorio-para-la-minera/blob/main/columna%20flotacion%20limpia.jpg)

El proceso de flotación es un procedimiento de extracción de metal (hierro) a partir de su mineral. Se concentra el metal hasta que su ley sea adecuada (mínimo 60% de hierro) para uso en procesos metalúrgicos (hierro metálico y acero). Durante este proceso, en cada columna se trituran los minerales antes de mezclarlos con agua para convertirlos en pulpa; la superficie de esta pulpa es selectivamente convertida para repeler el agua a través del uso de reactivos específicos (amina, almidón). Luego los minerales de la pulpa se separan a través de un flujo de burbujas de aire que se adhieren a las partículas que repelen el agua para que floten y así son recolectadas en una espuma (partículas de sílica). Se espera que el contenido de la sílica al final del procesos se encuentre entre un rango ideal (entre  $0,5$% y 2%) para asegurar la calidad del concentrado de hierro.

## Descripción detallada del proyecto, propósito y contexto

Se cuenta con información entregada correspondiente a datos tabulados en un archivo de tipo csv. El conjunto de datos proviene de una planta de flotación con 737.453 observaciones ordenadas
y antiguas, entre marzo y septiembre de 2017. La dimensión de los datos es 24: reportando 23 variables simples cuantitativas de tipo flotante (continuas) y 1 variable fecha compuesta (discreta) inicialmente detectada como de tipo object por Pandas. Fecha considera el momento de cada medición realizada entre marzo y septiembre de 2017. En total hay 4097 instancias distintas de horas con alrededor de 174 a 180 muestras. El concentrado de sílica es la variable dependiente. En relación a la flotación se toman medidas antes de la planta de flotación, en el proceso de flotación y al final del proceso, y el objetivo es: a partir de los datos predecir el concentrado de sílica en el proceso (porcentaje concentrado de sílica medido al final del proceso en el laboratorio). Se asume que la variable a predecir es de tipo estática. Los restantes 23 atributos son: 

	\begin{table} 
			\begin{tabular}{|l|l|c|} \hline
				{\bf Característica} & {\bf Variable (o Atributo)} & {\bf Unidad} \\ \hline
				{\small Tiempo }   & $X_0:$ Fecha  &  Año-Mes-Día Hora:Minuto:Segundo \\ \hline
				{\small Medidas de calidad del mineral de hierro  justo antes de la planta de flotación}    & $X_1:$ Alimentación de hierro &   \% \\
				& $X_2:$ Alimentación de sílica  &   \%\\ \hline
				{\small  Medidas al final del proceso de flotación}    & $X_3:$ Flujo de almidón &  $\dfrac{m^3}{h}$ \\
				& $X_4:$ Flujo de amina &    $\dfrac{m^3}{h}$ \\
				&  $X_5:$ Flujo de pulpa mineral &   $\dfrac{t}{h}$ \\
				&  $X_6:$ pH de pulpa de mineral  &  no tiene \\
				& $X_7:$ Densidad de la pulpa de mineral  &  $\dfrac{kg}{cm^3}$  \\  \hline
				{\small Flujo de aire en el proceso de flotación}   &  $X_8:$ Flujo de aire columna de flotación 1  &  $\dfrac{Nm^3}{h}$ \\
				& $X_9:$ Flujo de aire columna de flotación 2  &  $\dfrac{Nm^3}{h}$ \\
				& $X_{10}:$ Flujo de aire columna de flotación 3  &   $\dfrac{Nm^3}{h}$\\
				& $X_{11}:$ Flujo de aire columna de flotación 4   &  $\dfrac{Nm^3}{h}$ \\
				&  $X_{12}:$ Flujo de aire columna de flotación 5 &  $\dfrac{Nm^3}{h}$ \\
				&  $X_{13} :$ Flujo de aire columna de flotación 6 &  $\dfrac{Nm^3}{h}$ \\
				& $X_{14} :$ Flujo de aire columna de flotación 7  &  $\dfrac{Nm^3}{h}$ \\   %\hline
				& $X_{15} :$ Nivel columna de flotación 1  &   $mm$\\
				& $X_{16} :$ Nivel columna de flotación 2  &   $mm$\\
				& $X_{17} :$ Nivel columna de flotación 3   &  $mm$ \\
				& $X_{18} :$ Nivel columna de flotación 4  &  $mm$ \\
				& $X_{19} :$ Nivel columna de flotación 5  &  $mm$ \\
				& $X_{20}:$ Nivel columna de flotación 6  &  $mm$ \\
				& $X_{21}:$  Nivel columna de flotación 7 &  $mm$  \\ \hline
				{\small Medida final de calidad de mineral de hierro mediante laboratorio}   &  $X_{22}:$ Concentrado de hierro &   \% \\
				& $Y:$ Concentrado de sílica  &   \%\\ \hline
			\end{tabular}
			\caption{\textsf{{\footnotesize Variables presentes en la fuente de datos, incluyendo sus unidades respectivas.}}}
			\label{tabla1}
		\end{table}

Alimentaci´on de hierro, Alimentaci´on de s´ılica, Flujo de amina, Flujo de pulpa mineral,
pH de pulpa mineral, Densidad de la pulpa de mineral, Flujo de aire en cada una de las 7 columnas de flotaci´on,
Nivel en cada una de las 7 columnas de flotaci´on y Concentrado de hierro, todas potenciales variables explicativas
provenientes de las observaciones. En el Cuadro 1 se detallan todas las variables.
Se verific´o que no hay datos faltantes, ni valores fuera de rango de los atributos seg´un lo investigado del proceso de
flotaci´on, de manera que a priori no hay valores imposibles ni atributos irrelevantes en cuesti´on. Se constat´o que todos
los datos corresponden al a˜no 2017 desde marzo a septiembre, con d´ıas desde 01 hasta 31, hora desde 00 hasta 23, con
00 minutos y 00 segundos. Por lo que el dato corresponde a las mediciones hechas a cada hora en los d´ıas de cada uno
de los meses enunciados.
Se detectaron 1171 datos duplicados, es decir, mismas mediciones en exactamente mismos momentos de muestra
(precisamente a la misma hora). Se excluyen los duplicados del an´alisis exploratorio quedando un conjunto de 736.282
datos, sin perjuicio de ser considerados en t´erminos comparativos para la obtenci´on del modelo de predicci´on en el
futuro. En t´erminos de justificar tal exclusi´on de duplicados podemos plantear que: ante el desconocimiento de las
tecnicidades del proceso, no se conoce en detalle la posibilidad real de tener estos duplicados consider´andose poco
probable tener estas coincidencias en el proceso por lo flujos din´amicos. Por otro lado, se desconoce la manipulaci´on
previa de los datos entregados, siendo los duplicados posibles errores de registro que representan solo alrededor del
0,15 % del dataset. As´ı, cada registro u observaci´on (fila) representa el conjunto de medidas (columnas) de una ´unica
medici´on en el proceso. Tambi´en se detectaron duplicados por columna, no obstante se consider´o no recomendable
excluirlos de la investigaci´on por la p´erdida de informaci´on del proceso que podr´ıa significar.
En el an´alisis se efect´ua un estudio de potenciales outliers con diversas estrategias de remoci´on. Se considera un dato
at´ıpico a aquel que, en general, se encuentran fuera del intervalo [Q1 − 1, 5 ∗ RIQ, Q3 + 1, 5 ∗ RIQ], donde Q1 y Q3
corresponden al primer y tercer cuartil respectivamente, RIQ = Q3−Q1 es el rango intercuart´ılico (largo de la caja en
el boxplot), para detalles ver c´odigo en archivo adjunto extensi´on .ipynb donde se exhibe un m´etodo creado a trav´es de
un ciclo for que elimina outliers columna a columna junto a otro m´etodo de puntuaci´on Z. Al probar estas dos formas
de remoci´on se obtuvieron estad´ısticos, histogramas y correlaciones muy similares al an´alisis exploratorio original con
los outliers (sin duplicados), ya que lograron remover un porcentaje muy peque˜no de datos. Se localiz´o un tercer
m´etodo de modo de remover un porcentaje mayor para contrastar los modelos a evaluar en este informe. Este m´etodo
aplica la funci´on stats.iqr de la librer´ıa scipy que ejecuta horizontalmente la remoci´on. As´ı, se obtiene la detecci´on de
203.029 potenciales outliers correspondiente al 27.57 % de los datos con la exclusi´on de las filas duplicadas.

Se presenta un breve análisis exploratorio indagando medidas de centralidad y de extensión. Se exhibe un análisis para entender y modelar cómo el porcentaje de sílica se ve afectado por los otros factores del proceso de flotación, el cual es realizado para disminuir la concentración de sílica presente en el mineral de hierro. Este análisis considera una descripción de los datos de tipo general, relaciones y comparaciones pertinentes tipo scatter plot, boxplot y correlaciones lineales. Esto en virtud de poder entrever alguna hipótesis para el objetivo planteado de predecir el porcentaje de concentración final de sílica. Se hace un estudio habitual de posibles outliers a través de boxplot exponiendo el análisis exploratorio de forma comparativa con y sin potenciales outliers. El estudio es efectuado en virtud de lo aprendido en un curso de Fundamentos de Ciencia de Datos. 


## Tecnologías Utilizadas

Los análisis expuestos hacen uso de las librerías pandas, numpy, datatime, matplotlib, seaborn, scipy y sklearn en lenguaje de programación Python
con Notebook de Jupyter. 

## Instalación

[Instrucciones claras sobre cómo instalar y configurar el proyecto localmente, incluyendo las dependencias si es necesario]

## Uso

[Instrucciones sobre cómo utilizar el proyecto, incluyendo ejemplos y comandos si aplican]

## Resultados

[Detalles sobre los resultados clave obtenidos durante el proyecto, posiblemente acompañados de gráficos o visualizaciones]

## Aprendizajes

[Comparte tus aprendizajes, desafíos superados y reflexiones personales durante el proyecto]

## Contribución

[Instrucciones para aquellos que deseen contribuir al proyecto o informar sobre problemas]

## Licencia

[Indica la licencia bajo la cual se publica el proyecto]

---

[Opcional: Agrega cualquier información adicional, enlaces a recursos externos o créditos]

[Incluye una sección de contacto si deseas que las personas se pongan en contacto contigo para obtener más información]

