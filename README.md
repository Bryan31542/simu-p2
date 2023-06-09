# Questions

## 1. ¿Por qué el contorno es 2D se vuelve un concepto más intuitivo?

El contorno en el contexto del método de los elementos finitos en 2D se vuelve más intuitivo debido a que estamos trabajando en un espacio bidimensional, lo que significa que estamos considerando problemas que involucran objetos y geometrías planas.

En 2D, los contornos son líneas o curvas que delimitan la geometría o el dominio del problema. Estos contornos pueden representar bordes de objetos, fronteras de regiones o límites físicos en el problema que estamos analizando.

## 2. Al hablar de condiciones de contorno, ¿qué limitación encontrada en 1D desaparece al trabajar en 2D?

En 1D, la geometría se reduce a una línea recta, y las condiciones de contorno se aplican solo en los extremos de esa línea. Por lo tanto, las condiciones de contorno en 1D generalmente se expresan como valores conocidos en esos dos puntos finales, como desplazamientos, fuerzas o temperaturas fijas.

Sin embargo, en 2D, tenemos una geometría más rica y compleja, y podemos tener contornos con características variables en diferentes partes del dominio. Podemos definir condiciones de contorno no solo en los bordes o límites externos de la geometría, sino también en líneas internas o curvas dentro del dominio.

## 3. ¿Cómo se construye la Tabla de Conectividades en 2D?

Ya que estamos trabajando con triángulos cada uno de sus vértices ahora será un nodo. Además, cada triángulo tendrá tres nodos y estarán indicados en los indices de nuestra columnas, mientras que en los indices de nuestras filas estarán las cantidad de elementos de nuestra malla.

Cabe recalcar que es necesario escoge un sentido para realizar la numeración de nodos

- Clockwise
- Counterclockwise

|       | **1** | **2** | **3** |
| ----- | ----- | ----- | ----- |
| **1** |       |       |       |
| **2** |       |       |       |
| **3** |       |       |       |
| **4** |       |       |       |

## 4. ¿Por qué es importante seleccionar un sentido al momento de construir la Tabla de Conectividades?

Asegura la coherencia y consistencia en los cálculos, matrices y vectores generados. Asi como en las condiciones de contorno y la interpretación visual de los resultados.

## 5. ¿Qué ocurre si no se es consistente con el sentido seleccionado al construir la Tabla de Conectividades

Los resultado obtenidos no serán precisos y confiables. Lo que complicará el comprender la geometría y comportamiento físico del problema analizado.

## 6. Explique cómo el mallado en 2D presenta una alta variabilidad en la definición formal del dominio.

Es posible utilizar triángulos, cuadriláteros o incluso formas más complejas para representar los elementos de la malla. La cantidad de nodos y elementos es totalmente variable, asi como el tamaño de los elementos.

## 7. Describa en qué consiste la iso-parametrization. ¿En qué conceptos se basa?

Consiste el pasar de un sistema de referencia a otro, ya que es necesario ocupar otro eje de coordenadas debido a que cada triángulo generado dentro de la malla es distinto. Tanto en tamaño, orientación u otras cualidades. Hay que pasar de coordenadas en (x, y) a coordenadas en (ξ, η). Lo que permite generalizar en comportamiento de cada elemento de la malla.

A partir de la iso-parametrization se crear un elemento localizado

Hay garantía de que cualquier elemento real puede ser transformado en este elemento ideal

Las funciones de forma se definen en base a este elemento ideal

## 8. ¿Cuáles son las Funciones de Forma que se utilizan en el MEF en 2D? ¿Por qué se utilizan precisamente estas definiciones?

N1 = 1 - ξ - η

N2 = ξ

N3 = η

Son funciones de forma lineales que cumplen con las condiciones de interpolación y son coherentes con la geometría del elementos

## 9. Al integrar el término independiente (el que contiene el valor Q), ¿cuál fue el problema descubierto? ¿Por qué es un problema? ¿Qué concepto se utilizó para resolverlo?

Ya que las funciones de forma fueron generadas a partir de la iso-parametrization el sistema con el que se está realizando la integración no concuerda ya que:

dA = dxdy

Y el sistema de las funciones de forma se encuentra en (ξ, η)

Por ende, es necesario introducir una transformación espacial, para ello hay que multiplicar una matriz por cada uno de los nodos de nuestro triángulo dicha matriz será denominada

Jacobian

## 10. Describa un proceso de transformación espacial en 2D

## 11. ¿Qué representa un Jacobian? ¿Qué contiene?

Representa la relación que existe entre las coordenadas originales en (x, y) y las coordenadas transformadas en (ξ, η).

El Jacobian se calcula como la matriz de derivadas parciales de las coordenadas físicas respecto a las coordenadas paramétricas

## 12. ¿Para qué se utiliza el Jacobian en el MEF?

Es utilizado en el MEF para realizar la transformación entre el espacio físico y el espacio paramétrico, calcular derivadas espaciales, y realizar integración numérica en el dominio paramétrico. Es una herramienta clave para relacionar la geometría física del problema con la formulación matemática del MEF y obtener soluciones precisas y confiables.

## 13. ¿Para qué se llevó a cabo la interpolación de las variables espaciales X e Y?

//TODO: tiene que ver con el Jacobian

El Jacobian actúa como un factor de escala que permite mover o transformar las coordenadas del plano (x, y) al plano (ξ, η). Además, es una transformación linar y debido en el área no nos interesa los signos negativos de la reflexión se utilizan el valor absoluto del Jacobian

## 14. ¿Cómo se definieron los límites de integración de las integrales dobles del proceso del MEF? ¿Por qué son esos valores y no otros?

Ahora el diferencial es

dξdη

Por ende la integral externa corresponde a η y η estará variando desde 0 hasta 1

Mientras que la integral interna corresponde a ξ, la cual va desde 0 hasta la recta

η = mξ + b

1 = m(0) + b -> b = 1

0 = m(1) + 1 -> m = -1

η = -ξ + 1

ξ = 1 - η

## 15. Al integrar el término correspondiente a la matriz de coeficientes (el que contiene las variaciones espaciales de N), ¿cuáles fueron los problemas descubiertos? ¿Por qué constituyen un problema? ¿Qué conceptos se utilizaron para resolverlos?

Ya que ∇N corresponde a las derivadas parciales con respecto a (x, y) y nuestra matriz de funciones de forma se encuentra en otro sistema de coordenadas (ξ, η) el resultado de dicha derivación da cero.

Entonces se aplica el Jacobian inverso J^-1 para lograr (∂/∂ξ) y (∂/∂η)

Lo que permite continuar con el proceso de integración en un mismo eje de coordenadas

## 16. Reflexione, ¿es más probable en 2D que las K y las b locales sean diferentes entre elementos?

Si, es más probable. Esto ocurre debido a la tabla de conectividad, ya que puede ser elaborada de muchas maneras, siempre y cuando se respete la orientación. Además, cada elemento ahora tendrá un área y Jacobian distinto para armar la matriz **K** y un **J** distinto para la matriz **b**

## 17. ¿Qué problema se presentó relacionado a la notación de super-índices?

![one](./img/1.png)

Es posible que existe una confusión cuando se hable de un elemento local, entonces

**J^2** es sustituido por **J \* J**, lo que permite que ahora cada super índice sea utilizado para denotar el número del elemento.

## 18. Para el área de un triángulo, ¿por qué no usamos la fórmula tradicional de (base\*altura)/2?

Si se intentará utilizar las fórmula de base por altura se necesita establecer vectores desde cada uno de los vertices del triángulo y buscar que dichos vectores se interceptados y que sean perpendiculares entre ellos. Lo que convierte el proceso en algo muy tedioso y extenso de realizar.

Por ende, se procede a utilizar la siguiente fórmula que contempla (x1, y1), (x2, y2) y (x3, y3), ya que desde un inicio se conocen los vertices de cada triángulo

![two](./img/2.png)

## 19.  Al utilizar la notación de barras (| |), ¿cómo diferenciamos si se trata de un valor absoluto o el determinante de una matriz?

Se trata de un valor absoluto cuando el contenido sea un escalar, mientras que se hace referencia al determinante de una matriz si el contenido es una **matriz** 

## 20. ¿Por qué, a pesar de lo distinto que se conforma la K con respecto a 1D, siempre queda simétrica?

Porque se están multiplicando matrices por su transpuesta lo que da como resultado una matriz simétrica

## 21.  En sus palabras, ¿por qué el proceso de ensamblaje es básicamente el mismo en 2D en comparación a 1D?

Debido a que dicho proceso de ensamblaje se realiza a partir de una tabla de conectividad. Además, el MEF indica una serie de pasos a seguir, por ende los pasos serán los mismos sin importar las dimensiones del fenómeno.

## 22. ¿Cuáles con las consideraciones adicionales a tomar en cuenta en el ensamblaje 2D?

Que las ahora los elementos ya no son contiguos, por ende hay que prestan mucha atención a los indices de la matriz contrastando con la tabla de conectividad 

## 23. ¿Por qué el proceso de aplicación de las condiciones de contorno es básicamente el mismo en 2D en comparación a 1D?

Debido a que se está utilizando el MEF y se siguen sus pasos. El cambio que puede surgir es la cantidad de nodos a los que se le aplican dichas condiciones de contorno, ya que puede ser mayor a 1.

## 24. ¿Cuáles con las consideraciones adicionales a tomar en cuenta en el proceso de aplicación de las condiciones de contorno en 2D?

Que ahora aumenta en número de nodos en los que pueden ser aplicadas las condiciones, lo que indica que es posible eliminar más de una fila por **Dirichlet** y la matriz que se suma al lado derecho puede tener más de un elemento no nulo debido a **Neumann**

## 25. ¿Por qué es importante la interpretación de resultados?

Porque el MEF unicamente nos brinda datos. Es necesario analizarlos e interpretarlos para comprender el fenómeno que se esta analizando.