---
layout: page
title: Manual
permalink: /manual
comments: false
---

----

# Manual de uso del módulo PyElectrica

---

---

Esta página se presenta como un manual de uso del módulo PyElectrica. La página contiene el ejemplo de uso de cada una de las funciónes disponibles en el módulo en la versión actual.

---

## << CIRCUITOS ELÉCTRICOS >>

---

### Función leyOhm


```python
from pyelectrica import leyOhm
help(leyOhm) 
```

    Help on function leyOhm in module pyelectrica.pyelectrica:
    
    leyOhm(**param)
        Función para calcular la Ley de Ohm, en base al parámetro
        con incognita '?'.
        
        Ejemplo:
        leyOhm(V='?', I=3, R=4)
        
        V = Valor de tensión
        I = Valor corriente
        R = Valor de resistencia
        
        IMPORTANTE: Se debe indicar dos valores numericos y el valor
                    que se quiere calcular indicando su valor con la
                    cadena de texto: '?'
        
                    Ejemplo:
                    # Para calcular el voltaje:
                    leyOhm(V='?', I=3, R=4)
        
                    # Para calcular la resistencia:
                    leyOhm(V=24, I=3.5, R='?')
        
                    # Para calcular la corriente:
                    leyOhm(V=12, I='?', R=5)
        
                    ** La función acepta números complejos **
    



```python
leyOhm(V=24, I='?', R=3.5) 
```

    I = 6.857 A



```python
leyOhm(V='?', I=3+35j, R=2+5j) 
```

    V = (-169+85j) V


---

### Función vNodos


```python
from pyelectrica import vNodos
help(vNodos) 
```

    Help on function vNodos in module pyelectrica.pyelectrica:
    
    vNodos(A, B)
        Función vNodos, que resuelve un sistema de ecuaciones en forma
        matricial y entrega los correspondientes voltajes de nodo en base
        al sistema de ecuaciones del circuito.
        
        Ejemplo:
        vNodos(A, B)
        
        A = lista que define la matriz de coeficiente.
        B = lista que define la matriz del vector solución.
    



```python
A = [
    [1+3j, 2+2j, 3+5j],
    [4+2j, 0, 6+2j],
    [7+2j, 8+6j, 0]
]
B = [
    [18+25j],
    [15+35j],
    [12+40j]
]
vNodos(A, B)  
```

    Los voltajes de nodo del circuito son:
    
    v1 = (-3.758+10.622j) Volts
    v2 = (3.154-5.72j) Volts
    v3 = (7.693-2.56j) Volts


---

### Función "iLazos" e "iLazosV"


```python
from pyelectrica import iLazos, iLazosV
help(iLazos) 
```

    Help on function iLazos in module pyelectrica.pyelectrica:
    
    iLazos(A, B)
        Función iLazos, que resuelve un sistema de ecuaciones en forma
        matricial y entrega las correspondientes corrientes de lazo en base
        al sistema de ecuaciones del circuito.
        
        Ejemplo:
        iLazos(A, B)
        
        A = lista que define la matriz de coeficiente.
        B = lista que define la matriz del vector solución.
    



```python
A = [
    [1, 0, 2, 8],
    [2, 9, 3, 7],
    [9, 2, 8, 4],
    [7, 4, 6, 5]
]
B = [
    [15],
    [-10],
    [0],
    [8]
]
iLazos(A, B) 
```

    Las corrientes de lazo del circuito son:
    
    i1 = 14.267 Amperes
    i2 = -1.872 Amperes
    i3 = -17.861 Amperes
    i4 = 4.557 Amperes


### Usando la función iLazosV

La función iLazosV entrega una matriz de resultados, los cuales pueden ser operados segun criterios personales de análisis. 



```python
corrientes = iLazosV(A, B) 
corrientes
```




    array([[ 14.26704545],
           [ -1.87215909],
           [-17.86079545],
           [  4.55681818]])




```python
i1 = corrientes[0,0] 
i1
```




    14.267045454545476




```python
r1 = 5.5
vx = i1 * r1
vx
```




    78.46875000000011




```python
print('El voltaje vx =', round(vx, 3), 'Volts') 
```

    El voltaje vx = 78.469 Volts


---

### Función "bode" y "bodeNb"


```python
from pyelectrica import bode
from pyelectrica import bodeNb
help(bode) 
```

    Help on function bode in module pyelectrica.pyelectrica:
    
    bode(num, den)
        Función que genera los diagramas de Bode para una función  de
        transferencia, indicada por su numerador (num) y denominador(den).
        
        Ejemplo:
        bode(num, den)
        
        num = valores en formato de lista, que contiene lo valores del
              númerador de la fución de transferencia.
        
        den = valores en formato de lista, que contiene los valores del
              denominador de la función de transferencia.
    



```python
num = [-0.1,-2.4,-181,-1950]
den = [1,3.3,990,2600] 
```


```python
bode(num, den) 
```


![png](assets/images/manual/output_31_0.png)


#### Usando la función bodeNB

\* Función recomendada cuando se trabaja en Jupyter Notebook.

La función _bodeNB_ genera el mismo resultado que la función _bode_, con la excepción que el diagrama de amplitud y fase se generan en graficos separados para mejorar la visualización.


```python
bodeNb(num, den) 
```


![png](assets/images/manual/output_35_0.png)



![png](assets/images/manual/output_35_1.png)


---

### Función "escalon"


```python
from pyelectrica import escalon
help(escalon) 
```

    Help on function escalon in module pyelectrica.pyelectrica:
    
    escalon(num, den)
        Función escalón, para generar la respuesta escalón en base a una
        función de transferencia.
        
        Ejemplo:
        escalon(num, den)
        
        num = valores en formato de lista, que contiene lo valores del
              númerador de la fución de transferencia.
        
        den = valores en formato de lista, que contiene los valores del
              denominador de la función de transferencia.
    



```python
num = [25]
den = [1, 5, 50]
escalon(num, den) 
```


![png](assets/images/manual/output_39_0.png)


---

### Función "c_1orden"


```python
from pyelectrica import c_1orden
help(c_1orden) 
```

    Help on function c_1orden in module pyelectrica.pyelectrica:
    
    c_1orden(**kwarg)
        Función para calcular y dibujar la gráfica de la curva de respuesta
        en un circuito RC o RL sin fuente, tomando como base a los parámetros
        indicados en la función.
        
        Ejemplo1:
        c_1orden(Vi=18, R=4.5 C=0.1) * Para circuitos RC
        
        Ejemplo1:
        c_1orden(Ii=18, R=1.4, L=0.5) * Para circuitos RL
        
        Donde:
        R = Resistencia del circuito
        t = el tiempo máximo a tomar en cuenta para la grafica
            *(Para mejores efectos visuales: 1 > t < 10)
        Vi = Voltaje inicial en el capacitor
        Ii = Corriente inicial en el inductor
        C = Valor del capacitor
        L = Valor del inductor
    



```python
c_1orden(Vi=10, R=4.5, C=0.3) 
```


![png](assets/images/manual/output_43_0.png)


---

## << MÁQUINAS ELÉCTRICAS >>

---

### Función mLineal_CD


```python
from pyelectrica import mLineal_CD
help(mLineal_CD) 
```

    Help on function mLineal_CD in module pyelectrica.pyelectrica:
    
    mLineal_CD(Vb=120, R=0.5, l=1, B=0.5)
        Función "mLineal_CD", util para calcular el comportamiento de una
        máquina lineal CD en base a los parámetros declarados.
        
        Ejemplo:
        mLineal_CD(Vb, R, l, B)
        
        Vb = Voltaje de la batería
        R = Resistencia del diagrama de la máquina lineal CD
        l = longitud del conductor en el campo magnético
        B =  Vector de densidad de flujo magnético
    



```python
mLineal_CD(Vb=120, R=0.6, l=1, B=0.5) 
```


![png](assets/images/manual/output_49_0.png)


---

### Función "compCA_GenSinc"


```python
from pyelectrica import compCA_GenSinc
help(compCA_GenSinc) 
```

    Help on function compCA_GenSinc in module pyelectrica.pyelectrica:
    
    compCA_GenSinc(Sbase=100000000, Vbase=13800.0, Xs=1.0, X1p=0.25, X2p=0.12, T1p=1.1, T2p=0.04)
        Función "compCA_GenSinc" para calcular la componente CA de la
        corriente de falla de un generador síncrono en base a los
        parámetros ingresados.
        
        Ejemplo:
        compCA_GenSinc(Sbase, Vbase, Xs, X1p, X2p, T1p, T2p)
        
        Donde:
        Sbase = Potencia aparente del generador síncrono
        Vbase = Voltaje base del generador síncrono
        Xs = Reactancia síncrona del generador síncrono
        X1p = Reactancia transitoria
        X2p = Reactancia subtrancitoria
        T1p = Constante de tiempo de la corriente transitoria
        T2p = Constante de tiempo de la corriente subtrancitoria
    



```python
compCA_GenSinc(Sbase=100*10**6, Vbase=13.8*10**3, Xs=1.0, 
               X1p=0.25, X2p=0.12, T1p=1.1, T2p=0.04) 
```


![png](assets/images/manual/output_53_0.png)


---

### Función "par_vel"


```python
from pyelectrica import par_vel
```


```python
help(par_vel) 
```

    Help on function par_vel in module pyelectrica.pyelectrica:
    
    par_vel(Vn=460, Polos=4, R1=0.641, X1=1.106, R2=0.332, X2=0.464, Xm=26.3)
        Función "par_vel" para calcular y generar la gráfica de la curva
        Par-Velocidad de un motor de inducción con rotor devanado y/o
        rotor jaula de ardilla.
        
        Ejemplo:
        par_vel(Vn, Polos, R1, X1, R2, X2, Xm)
        
        Donde:
        Vn = Voltaje nominal del motor
        Polos = Número de polos del motor
        f = Frecuencia de operación del motor
        R1 = Resistencia del estator
        X1 = Reactancia del estator
        R2 = Resistencia del rotor
        X2 = Reactancia del rotor
        Xm = Reactancia de magnetización
    



```python
par_vel(Vn=460, Polos=4, R1=0.641, X1=1.106, R2=0.332, X2=0.464, Xm=26.3) 
```


![png](assets/images/manual/output_58_0.png)


---

### Función "cepTransformador"


```python
from pyelectrica import cepTransformador
```


```python
help(cepTransformador) 
```

    Help on function cepTransformador in module pyelectrica.pyelectrica:
    
    cepTransformador(Voc, Ioc, Poc, Vsc, Isc, Psc)
        Función "cepTransformador" para calcular el circuito equivalente de
        un transformador en el lado del primário, en función de sus parametros
        de las pruebas de circuito abierto y corto circuito.
        
        Ejemplo:
        cepTransformador(Voc, Ioc, Poc, Vsc, Isc, Psc)
        
        Donde:
        Voc = Voltaje en prueba de circuito abierto en el lado primario.
        Ioc = Corriente en prueba de circuito abierto en el lado primario.
        Poc = Potencia en prueba de circuito abierto en el lado primario.
        Vsc = Voltaje en prueba de corto circuito en el lado primario.
        Isc = Corriente en prueba de corto circuito en el lado primario.
        Psc = Potencia en prueba de corto circuito en el lado primario.
    



```python
cepTransformador(Voc=8000, Ioc=0.214, Poc=400, Psc=240, Vsc=489, Isc=2.5) 
```

    Rc 	 = 	 160.0 kOhms
    Xm 	 = 	 38.45 kOhms
    Req 	 = 	 38.4 Ohms
    Xeq 	 = 	 191.79 Ohms



![png](assets/images/manual/output_63_1.png)


---

## << INSTALACIONES ELÉCTRICAS>>

---

### Función "imonoF"


```python
from pyelectrica import imonoF
```


```python
help(imonoF)
```

    Help on function imonoF in module pyelectrica.pyelectrica:
    
    imonoF(VA, Vn)
        Función para calcular la corriente de un circuito eléctrico en el diseño
        de instalaciones eléctricas residenciales. La función también recomienda
        el calibre de cable adecuado para la corriente del circuito.
        
        Sintaxis:
        imonoF(VA, Vn)
        
        Donde:
        VA = Volt-Ampere de la carga o del circuito a calcular.
        Vn = Voltaje nominal de fase a neutro.
    



```python
imonoF(VA=2600, Vn=120)
```

    
    Para una carga de 2600 VA conectada a 120 V.
    La corriente calculada es de: 21.67 A.
    El calibre de cable recomendado es del #12 AWG, tipo THW o similar.


---

### Función "cTensionMono"


```python
from pyelectrica import cTensionMono
```


```python
help(cTensionMono)
```

    Help on function cTensionMono in module pyelectrica.pyelectrica:
    
    cTensionMono(l, I, Vn, c)
        Función cTension para calcular la caída de tensión en un conductor,
        utilizando la formula de caída de tensión de instalaciones eléctricas.
        
        Sintaxis:
        cTensionMono(l, I, Vn, c)
        
        Donde:
        l = Longitud hasta la última carga del circuito.
        I = Corriente que pasara en el conductor.
        Vn = Tensión nominal a neutro.
        c =  Calibre del conductor.
    



```python
cTensionMono(l=16, I=21.67, Vn=120, c=12)
```

    
    Los datos ingresados son los siguientes:
    La longitud del circuito es de 16 Mts.
    La corriente en el circuito es de 21.67 A.
    El voltaje de operación del circuito es de 120 V.
    El calibre del conductor seleccionado es del #12 AWG.
    La caída de tensión del circuito es de 3.49 %.


---






_"La forma más fácil de aprender algo, es practicándolo"_

_**Isai Aragón P.**_
