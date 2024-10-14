# Shark_Attack
En este primer proyecto trataremos de analizar el data set Shark Attacks para sacar las conclusiones a las hipotesis planteadas.             
A modo de resumen, el archivo Shark_Attacks contiene una base de datos de los ataques de tiburones realizados a lo largo de los años y categorizado segun especies, edad, paises, personas afectadas etc.. 
De manera que este proyecto intentara averiguar las siguientes hipotesis:

**a) Correlacion entre fatalidad y edad**

**b) Fatalidad segun la especie implicada en el ataque** 

**c) Tipo de especies segun el pais de ataque**

**d) Tipo de especies segun el pais y la actividad que estaba llevando acabo la victima**  

# Primeros pasos

Instalar las librerias necesarias para llevar acabo todo el trabajo de limpieza y visualización. 
Las librerias utilizadas han sido, **Pandas**, **Numpy**, **Regex**, **Matplotlib** y **Seaborn**.

Lo primero ha sido llevar a cabo un primer analisis exploratorio del data set para ver que tipo de datos contenia y como estaba organizado. Usando metodos como **head()**,**tail()**,**describe()** o **df.columns()**.
Despues de este analisis exploratiorio comienza el trabajo de limpieza.

# Primera limpieza del data set

Esta fase ha sido la que mas tiempo ha ocupado del proyecto, ya que, la gran mayoria de los datos tenian erratas, espacios en blanco, letras y numeros juntos, valores NAN etc..

De manera que, eliminamos los espacios en blanco en los nombres de las columnas para poder trabajar bien. Así como,las columnas que tenian datos duplicados usando el metodo **drop()**.

Buscamos valores NAN en el data set y como se distribuyen. Dado que, a partir de cierta fila son todo NAN, eliminamos esas filas.

Para buscar a partir de que fila hay nulos:

- **sharks_raw["Date"].isna().idxmax()***

Para eliminar esas filas:
- **sharks_raw.drop(sharks_raw.index[6302:], inplace=True)**

Reemplazamos el resto de NAN por el objeto "unknown". Como forma de poder categorizar esos valores nulos en caso de que mas adelante nos sean utiles. Buscamos duplicados en el data set y creamos una columna de indice unico.
 
# Segunda limpieza del data set

En esta fase limpiaremos y arreglaremos los valores dentro de las columnas necesarias para averiguar nuestras hipotesis.

-**Date**: Utilizamos regex para eliminar las letras que hay junto a las fechas. Luego visualizamos como se distribuye. Cogeremos un subset sin los valores desconocidos para seguir trabajando y poder sacar conclusiones.

![Datedist](Pictures\Datedist.png)

-**Country, Area, Location**: Arreglamos los objetos creando diccionarios y haciendo el update a traves del indice. Ademas, en el caso de los unknowns podemos suponer esos objetos gracias a las otras columnas. Por ultimo visualizamos su distribucion.

![Countrydist](Pictures\Countrydist.png)

-**Sex**: Arreglamos esta columna utilizando un diccionario y haciendo update por indice. A continuación visualizamos.

![Sexdist](Pictures\Sexdist.png)

-**Age**: Utilizamos regex y el metodo replace pasandole un diccionario para arreglar los datos. Luego visualizamos.
Cogeremos un subset con los años conocidos para seguir trabajando y poder sacar conclusiones.

![agecode](Pictures\agecode.png)

![Agedist](Pictures\Agedist.png)

-**Fatal (Y/N)**: Utilizamos regex para encontrar valores extraños y luego el metodo replace para arreglarlos. Luego visualizamos.

![fatalcode](Pictures\fatalcode.png)

![Fataldist](Pictures\Fataldist.png)

-**Species**: Utilizamos el metodo apply y lambda. De esta mnaera, cada vez que encuentre ciertos valores los modificara a lo que nos interesa, y de esta manera podremos categorizar correctamente las especies. Dado que hay muchos ataques en los que no tenemos datos de la especie, hacemos una suposicion para poder categorizarlos a traves de su tamaño. Por ultimo visualizamos y nos guardamos un subset con las especies conocidas.

![codespecie](Pictures\codespecie.png)

![Speciesdist](Pictures\speciesdist.png)

-**Activity**: Usaremos el mismo metodo que con las especies. Visualizamos y guardamos un subset con las actividades conocidas.

![Activitydist](Pictures\activitydist.png)

# Conclusiones

**a)** Visualizamos la correlacion entre fatalidad y edad. Podemos ver que la tendencia por edad es que los ataques no sean mortales teniendo el pico de ataques letales entre los 13 y los 25 años. Aun así, como veiamos en la distribución de fatality, la gran mayoria de ataques no fueron letales y la unica suposición que podemos tomar es que entre los 13 y los 18 años de edad tendría algo mas de sentido que los ataques fueran letales, ya que, se trataria de niños.

![fatalxage](Pictures\fatalxage.png)

**b)** Visualizamos la fatalidad segun la especie implicada en el ataque. 

Primeramente se observa que hay dos grandes grupos. El primer grupo es el que mas muertes ha causado y esta encabezado por:

-**Tiburon Blanco**

 -**Tiburon Tigre**

 -**Tiburon Toro**

El segundo grupo esta formado por las especies con mas ataques realizadas pero sin ser mortales:

 -**Tiburon Blanco**

 -**Especies indeterminadas de tiburon pequeñas**

 -**Especies indertminadas de tiburon medianas**

 -**Tiburon Tigre y Toro**

 ![fatalxspecie](Pictures\fatalxspecie.png)

 **c)** Agrupamos por pais para ver como se distribuyen las especies en el top 50 de los ataques, usamos como agregacion **max** y **value_counts**. Esto nos ayudará a ver la correlacion en el siguiente apartado

 ![groupbyC](Pictures\groupbyC.png)

 ![groupby2](Pictures\groupbyC2.png)

 ![groupby3](Pictures\groupbyC3.png)


**d)** Observamos que los paises donde mas concentracion de ataques respectivamente hay son:

-**USA**

-**Australia**

-**South Africa**

-**Papua / Brasil / Nueva Zelanda / Bahamas / Mexico**

Observamos que las activades que recibieron mas ataques respectivamente son :

-**Fishing**

-**Surfing**

-**Swimming**

-**Diving**

Observamos que la especie segun el pais y la actividad respectivamente es:

-**Tiburon Tigre**

-**Tiburon Toro**

-**Tiburon Blanco**

Visualizamos el top 50 de los ataques por pais, especie de tiburon y actividad mediante varios groupby usando como agregacion el maximo y el conteo de valores(ver codigo), el mas clarificador es el ultimo. Adicionalmente realizamos un histograma.


![groupby](Pictures\groupby.png)

![groupby1](Pictures\groupby1.png)

![groupby2](Pictures\groupby2.png)

Observamos que los paises donde hay mas ataques son **USA** y **Australia**, tal y como lo veiamos distribuido mas arriba. En cuanto a la especie, a diferencia de lo que veiamos anteriormente, en el top 50 los que mas ataques han provocado son los **Tiburones Tigre** y los **Tiburones Toro**. Y por ultimo, el grupo mas atacado es el que se encontraba **nadando** y luego **pescando / buceando** tal y como se observa en la distribucion de Activity

# Histogram

![hist](Pictures\hist.png)