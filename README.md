# Laboratorio 5 - Variabilidad de la Frecuencia Cardíaca (HRV) y balance autonómico

**Universidad Militar Nueva Granada**

**Asignatura:** Procesamiento Digital de Señales

**Estudiantes:** Dubrasca Martínez, Mariana Leyton, Maria Fernanda Castellanos

**Fecha:** 9 de noviembre del 2025

**Título de la práctica:** Variabilidad de la Frecuencia Cardíaca (HRV) y balance autonómico

# **Objetivos**
- Identificar cambios en el balance autonómico mediante análisis temporal de la variabilidad de la frecuencia cardíaca (HRV).

# **Parte A**
## ***Actividad simpática y parasimpática del sistema nervioso autónomo***

El sistema nervioso simpático se origina en la médula espinal, específicamente en la región torácica y lumbar. Este es el responsable de preparar al cuerpo para la acción en situaciones de estrés o emergencia, conocido como el mecanimo de defensa y huida.

Cuando se activa el sistema nervioso simpático, el cuerpo experimenta una serie de cambios fisiológicos. Algunos de ellos son:

**- Aumento de la frecuencia cardiaca**

**- Dilatación de las vias respiratorias**

**- Aumento de la sudoración**

Mientras que, el sistema nervioso parasimpático tiene su origen en el cerebro y en la región sacra de la médula espinal. Este se activa durante situaciones de calma y relajación. Su función principal es conservar energía y promover procesos de recuperación en el cuerpo.

Cuando el sistema nervioso parasimpático se activa, el cuerpo experimenta una serie de cambios que promueven la relajación y la recuperación. Algunos de estos cambios son:

**- Disminución de la frecuencia cardiaca**

**- Estimulación de la digestión**

**- Constricción de las pupilas**

Estas respuestas son esenciales para la restauración del equilibrio interno del cuerpo, permitiendo que se recupere y se mantenga en un estado óptimo de funcionamiento [1].

## ***Efecto de la actividad simpática y parasimpática en la frecuencia cardíaca***

El corazón está inervado por nervios simpáticos y parasimpáticos. Los nervios parasimpáticos (vagos) se distribuyen principalmente a los nódulos sinoauricular y auriculoventricular, y los nervios simpáticos se distribuyen en todas las regiones del corazón con una intensa representación en el músculo ventricular.

La estimulación de los nervios ***parasimpáticos*** que llegan a los nodulos principalmente (los vagos) hace que se libere la hormona acetilcolina en las terminaciones nerviosas. Esta hormona tiene dos efectos principales sobre el corazón:

**- Reduce la frecuencia del impulso que genera el nódulo sinusal.**

**- Reduce la excitabilidad de las fibras de la unión AV entre la musculatura auricular y el nódulo AV, retrasando de esta manera la transmisión del impulso cardíaco hacia los ventrículos.**


La estimulación ***simpática*** produce esencialmente los efectos contrarios sobre el corazón a los que produce la estimulación vagal, en esta se libera la hormona noradrenalina, la cual estimula los receptores β1-adrenérgicos, que median en los efectos sobre la frecuencia cardíaca aumentando la permeabilidad de la membrana a iones positivos, esto provoca.

**- Aumenta la frecuencia de descarga del nódulo sinusal.**

**- Aumenta la velocidad de conducción, así como el nivel de excitabilidad de todas las porciones del corazón.**

**- Aumenta mucho la fuerza de contracción de toda la musculatura cardíaca, tanto auricular como ventricular** [2].



## ***Variabilidad de la frecuencia cardíaca (HRV) obtenida a partir de la señal electrocardiográfica (ECG)***

La variabilidad de la frecuencia cardíaca (HRV) es un reflejo directo de la modulación del sistema nervioso autónomo sobre el corazón. El aumento del tono parasimpático incrementa la variabilidad entre los intervalos R-R en el ECG, mientras que la activación simpática disminuye dicha variabilidad al generar una respuesta cronotrópica positiva. Por lo tanto, la HRV es un indicador sensible del equilibrio simpático-parasimpático y permite evaluar la función autonómica cardíaca en condiciones de reposo, estrés o actividad física. El análisis de la HRV obtenido del ECG es una herramienta fundamental en la fisiología cardiovascular, ya que permite inferir el estado autonómico y predecir alteraciones del sistema cardiovascular asociadas a predominio simpático, como la hipertensión, la dislipidemia, la diabetes o el sedentarismo [3].

## ***Diagrama de Poincaré como herramienta de análisis de la serie R-R***

El diagrama de Poincaré, también llamado diagrama de dispersión, es uno de los métodos no lineales más utilizados para evaluar la variabilidad de la frecuencia cardíaca (VFC). Este gráfico se construye representando cada intervalo R-R en función del siguiente, de modo que cada punto del plano corresponde a un par de intervalos consecutivos (RRn , RRn+1). Esta visualización permite analizar la estructura interna de la serie temporal y la relación latido a latido. El diagrama de Poincaré ofrece varias ventajas:

**- Permite identificar patrones no lineales en los intervalos R-R.**

**- Facilita la observación directa de la variación instantánea entre latidos.**

**- No requiere un preprocesamiento complejo.**

**- Conserva una alta correlación con medidas espectrales de la VFC.**

**- Puede revelar comportamientos dinámicos que no son evidentes con métodos lineales.**

En condiciones normales, el diagrama produce una nube de puntos alineada aproximadamente con la línea de identidad, que corresponde a los casos donde la duración de un intervalo es igual a la del siguiente. Los puntos situados por encima de esta línea representan intervalos más largos que el anterior (RRn < RRn+1) mientras que los puntos situados por debajo indican intervalos más cortos (RRn > RRn+1)

La forma de la nube puede aproximarse mediante una elipse cuyos ejes permiten cuantificar la variabilidad:

**-SD1** representa la dispersión perpendicular a la línea identidad (eje corto). Este parámetro refleja cambios rápidos y variabilidad de corto plazo, asociados principalmente con la actividad parasimpática.

**-SD2** corresponde a la dispersión a lo largo de la línea identidad (eje largo). Describe variaciones de largo plazo y está más ligado a la modulación simpática y a tendencias globales de la frecuencia cardíaca [4].
## ***Diagrama de flujo***

<img width="1760" height="1360" alt="_Diagrama de flujo -  Diagrama de flujo (3)" src="https://github.com/user-attachments/assets/3e1f4bd8-9b37-461f-8835-f5c16607a77b" />

## ***Adquisición de la señal***

## **Código en Python (Google colab)**
<pre>
voltaje = np.loadtxt("ECG_captura.txt")

# Definir parámetros de muestreo
fs = 500
N = len(voltaje)
t = np.arange(N) / fs  # eje de tiempo

# Graficar
plt.figure(figsize=(10,4))
plt.plot(t, voltaje, label="Señal ECG tomada")
plt.xlabel("Tiempo [s]")
plt.ylabel("Voltaje [V]")
plt.title("Señal ECG tomada")
plt.grid(True)
plt.show()
</pre>

## **Grafica de la señal**
<img width="846" height="395" alt="image" src="https://github.com/user-attachments/assets/6ea23a1c-16fb-41ab-8201-618bf29ab948" />

# **Parte B**
## *Punto C*

## **Código en Python (Google colab)**
<pre> ```
from google.colab import files
import numpy as np
import matplotlib.pyplot as plt
from scipy.signal import butter, lfilter
from scipy.signal import find_peaks
import os
uploaded = files.upload()
  
voltaje = np.loadtxt("ECG_captura.txt")
fs = 500
N = len(voltaje)
t = np.arange(N) / fs  
señal = np.loadtxt("ECG_captura.txt")
  
# Graficar los primeros 20 s
t = np.arange(len(señal)) / fs
lim = int(min(len(señal), int(20*fs)))
plt.figure(figsize=(10,6))
plt.subplot(2,1,1)
plt.plot(t[:lim], señal[:lim])
plt.title("ECG original (primeros 20 s)")
plt.xlabel("Tiempo [s]")
plt.ylabel("Voltaje [V]")
  ```
</pre>
## **Gráfica de los primeros 20 segundos de la señal ECG**
<img width="1115" height="335" alt="image" src="https://github.com/user-attachments/assets/d26303e3-8cf0-46b2-bbfb-217356519617" />

## **Filtro IIR**

## **Código en Python (Google colab)**
<pre> ```
fs = 500            # Frecuencia de muestreo [Hz]
lowcut = 0.5        # Corte inferior [Hz]
highcut = 40        # Corte superior [Hz]
order = 4           # Orden del filtro
 
b, a = butter(order, [lowcut/(0.5*fs), highcut/(0.5*fs)], btype='band')
b = np.array(b, dtype=float)
a = np.array(a, dtype=float)
if a[0] != 1.0:
    b = b / a[0]
    a = a / a[0]
  
print("Coeficientes del filtro Butterworth pasa-banda (orden 4)")
print("b =", np.round(b, 12))
print("a =", np.round(a, 12))
print()

print("Ecuación en diferencias forma general:")
print("y[n] = b0*x[n] + b1*x[n-1] + ... + bM*x[n-M] - (a1*y[n-1] + ... + aN*y[n-N])")
print()

def filtrar_iir_manual(x, b, a):
 # Implementa un filtro IIR mediante la ecuación en diferencias. Se asumen los parametros iniciales en 0.
    x = np.asarray(x, dtype=float)
    Nsig = len(x)
    M = len(b) - 1
    N = len(a) - 1
    y = np.zeros(Nsig, dtype=float)
    for n in range(Nsig):
        acc_num = 0.0
        for k in range(M + 1):
            if n - k >= 0:
                acc_num += b[k] * x[n - k]
        acc_den = 0.0
        for k in range(1, N + 1):
            if n - k >= 0:
                acc_den += a[k] * y[n - k]
        y[n] = acc_num - acc_den
    return y
  
y_filtrada = filtrar_iir_manual(sig, b, a)
np.savetxt("ecg_datos_filtrados.txt", y_filtrada)
print("Señal filtrada guardada como 'ecg_datos_filtrados.txt'.")

t = np.arange(len(sig)) / fs  # eje de tiempo
plt.figure(figsize=(10, 4))
plt.plot(t, y_filtrada, linewidth=0.8)
plt.title("Señal ECG filtrada (4 minutos)")
plt.xlabel("Tiempo [s]")
plt.ylabel("Voltaje [V]")
plt.grid(True)
plt.xlim(0, 240) 
plt.tight_layout()
plt.show()

  ```
</pre>
## **Gráfica de la señal ECG filtrada (4 minutos)**
<img width="1108" height="437" alt="image" src="https://github.com/user-attachments/assets/d5024dc9-72aa-49aa-88bc-12eeb62cb233" />

## **Gráfica de los primeros 20 segundos de la señal ECG filtrada**
<img width="1108" height="329" alt="image" src="https://github.com/user-attachments/assets/5068c869-d917-4908-8abd-5028ec25aaaf" />

## **Coeficientes del filtro IIR Butterworth pasa-banda de orden 4:**

b = [0.0021388, 0, -0.00855519, 0, 0.01283279, 0, -0.00855519, 0, 0.0021388]

a = [-6.69800177, 19.67771811, -33.14948678, 35.05040143, -23.83043337, 10.17602978, -2.49522749, 0.2690001]

Teniendo en cuenta la forma general de la ecuación en diferencias: y[n] = b0x[n] + b1x[n-1] + ... + bMx[n-M] - (a1y[n-1] + ... + aNy[n-N])

Al sustituir los coeficientes la ecuación de diferencias quedaria: 

**y[n] = 0.0021388x[n] + 0x[n-1] -0.00855519x[n-2] + 0x[n-3] + 0.01283279x[n-4] + 0x[n-5] -0.00855519x[n-6] + 0x[n-7] + 0.0021388x[n-8] -(-6.69800177y[n-1] + 19.67771811y[n-2] -33.14948678y[n-3] + 35.05040143y[n-4] -23.83043337y[n-5] + 10.17602978y[n-6] -2.49522749y[n-7] + 0.2690001y[n-8])**

## **Explicación del filtro IIR:**

El filtro fue diseñado como un IIR Butterworth de orden 4 y pasa-banda con cortes entre 0.5 y 40 Hz porque ese rango contiene la información fisiológica real del ECG, además que está alineada con los estándares biomédicos de adquisición de ECG según la [AHA (American Heart Association)](https://www.heart.org/).

Los 0.5 Hz eliminan la derivada de la línea base, el movimiento y respiración, pero conserva las ondas T y P que son las ondas que tienen baja frecuencia, mientras que los 40 Hz eliminan gran parte del ruido muscular, interferencias electrónicas y artefactos sin distorsionar el complejo QRS.

El tipo Butterworth se seleccionó para evitar ondulaciones en la banda pasante y preservar la forma de onda cardiaca, esto es muy importante debido a que el ECG preserva la forma de la onda sin distorsiones, especialmente del complejo QRS. Y de orden 4, ya que nos permite realizar un buen rechazo de ruido y estabilidad computacional sin riesgo de oscilaciones ni distorsión, lo que lo hace adecuado para procesar señales ECG en tiempo real.

El filtro se diseñó con la función ***butter*** de SciPy utilizando la representación en coeficientes directos (b y a) tras normalizar los bordes de banda respecto a la frecuencia de Nyquist (0.5·fs). Luego se verificó que el coeficiente a [0] fuera igual a 1 y, de no ser así, se normalizaron los arreglos para cumplir la forma estándar de la ecuación en diferencias. Finalmente, la señal se filtró, acumulando las contribuciones de muestras actuales y pasadas (parte numérica) y restando las contribuciones de salidas anteriores (parte recursiva), obteniendo así una señal ECG limpia dentro del intervalo útil de 0.5–40 Hz.

## **Division de la señal en dos segmentos y calculos de los intervalos de los picos R-R:**

## **Código en Python (Google colab)**
<pre> ```
señ_filt = np.loadtxt("ecg_datos_filtrados.txt")
N = len(señ_filt)
t = np.arange(N) / fs
duracion_total = N / fs
  
# División de la señal en dos segmentos
segmento1 = señ_filt[:int(120 * fs)]
segmento2 = señ_filt[int(120 * fs):int(240 * fs)]
t1 = np.arange(len(segmento1)) / fs
t2 = np.arange(len(segmento2)) / fs + 120

# Detección de picos R
picos1 = find_peaks(segmento1, height=np.mean(segmento1)+0.5*np.std(segmento1), distancia=300) # Se utiliza el parámetro "distancia" para evitar detectar varios picos dentro de un mismo latido
picos2 = find_peaks(segmento2, height=np.mean(segmento2)+0.5*np.std(segmento2), distancia=300)

# Calculo de los intervalos R-R
RR1 = np.diff(picos1) / fs  # en segundos
RR2 = np.diff(picos2) / fs
t_RR1 = t1[picos1[:-1]] + np.diff(t1[picos1]) / 2
t_RR2 = t2[picos2[:-1]] + np.diff(t2[picos2]) / 2

print(f"Segmento 1: {len(picos1)} picos R detectados")
print(f"Promedio RR (seg 1): {np.mean(RR1):.3f} s -> {60/np.mean(RR1):.1f} lat/min")
print(f"Segmento 2: {len(picos2)} picos R detectados")
print(f"Promedio RR (seg 2): {np.mean(RR2):.3f} s -> {60/np.mean(RR2):.1f} lat/min")
  ```
</pre>

## **Resultados:**
***Segmento 1: 130 picos R detectados***

***Promedio R-R: 0.930 segundos lo que corresponde a 64.5 lat/min***

***Segmento 2: 144 picos R detectados***

***Promedio R-R: 0.826 segundos lo que corresponde a 72.6 lat/min***

## **Código en Python (Google colab)**
<pre> ```
plt.figure(figsize=(12, 6))

# ECG Segmento 1
plt.subplot(3, 1, 1)
plt.plot(t1, segmento1, label='Segmento 1 (0–120 s)')
plt.plot(t1[picos1], segmento1[picos1], 'r*', label='Picos R')
plt.title("Segmento 1 – ECG filtrado con detección de picos R")
plt.xlabel("Tiempo [s]")
plt.ylabel("Voltaje [V]")
plt.legend()
plt.grid(True)

# ECG Segmento 2
plt.subplot(3, 1, 2)
plt.plot(t2, segmento2, label='Segmento 2 (120–240 s)')
plt.plot(t2[picos2], segmento2[picoss2], 'r*', label='Picos R')
plt.title("Segmento 2 – ECG filtrado con detección de picos R")
plt.xlabel("Tiempo [s]")
plt.ylabel("Voltaje [V]")
plt.legend()
plt.grid(True)

# Señales RR
plt.subplot(3, 1, 3)
plt.plot(t_RR1, RR1, 'b-o', label='RR Segmento 1')
plt.plot(t_RR2, RR2, 'g-o', label='RR Segmento 2')
plt.title("Variabilidad de los intervalos R–R")
plt.xlabel("Tiempo [s]")
plt.ylabel("Intervalo R–R [s]")
plt.grid(True)
plt.legend()

plt.tight_layout()
plt.show()
  ```
</pre>
## **Gráfica primer segmento ECG**
<img width="1335" height="221" alt="image" src="https://github.com/user-attachments/assets/da2ac8b5-8fbc-4d6b-b315-1a92a62d320c" />

## **Gráfica segundo segmento ECG**
<img width="1328" height="236" alt="image" src="https://github.com/user-attachments/assets/b76e6011-724c-49f8-acc1-fecd9659e4e9" />

## **Gráfica variabilidad de los intervalos R-R**
<img width="1335" height="216" alt="image" src="https://github.com/user-attachments/assets/385609e6-39b3-4925-9e3e-901ecd08b218" />

## **Explicación detección de picos y calculo de los intervalos:**
La señal ECG filtrada se dividió en dos segmentos de 2 minutos y luego se identificaron los picos R en cada segmento usando la función ***find_peaks***, que detecta los máximos más altos del ECG. Para asegurarse de que solo se detectara un pico R por latido, se estableció una altura mínima basada en el promedio y la desviación estándar de la señal, y un valor de distancia mínima de 300 muestras, lo que corresponde a 0.6 segundos a 500 Hz, evitando confundir pequeños picos cercanos con latidos reales. Después de detectar los picos, se calcularon los intervalos R-R midiendo el tiempo entre un pico R y el siguiente; esto se hizo restando las posiciones de los picos consecutivos y dividiendo por la frecuencia de muestreo para obtener los intervalos en segundos. 

## *Punto D*
## **Comparación de los valores de los parámetros básicos de la HRV en el dominio del tiempo:**

- **SDNN (desviación estandar de los intervalos R-R):**

- *Rango saludable o excepcional:*

- Mayor a 110 ms: excepcional

- 70 - 110 ms: saludable

- *Rango peocupante:*
  
- Menor a 50 ms: alto riesgo [5] [6].

## **Código en Python (Google colab)**
<pre> ```
media_RR1 = np.mean(RR1)
media_RR2 = np.mean(RR2)

sdnn1 = np.std(RR1)
sdnn2 = np.std(RR2)

print("\nParametros de la HVR en el dominio del tiempo")
print("Segmento 1 (0–120 s):")
print(f"    Media RR   : {media_RR1:.4f} s")
print(f"    SDNN       : {sdnn1:.4f} s")

print("Segmento 2 (120–240 s):")
print(f"    Media RR   : {media_RR2:.4f} s")
print(f"    SDNN       : {sdnn2:.4f} s")
  
  ```
</pre>
## **Resultados:**

*Segmento 1 (0-120 s):*

- Media R-R: 0.9298 s
  
- SDNN:      0.1327 s (132.7 ms)

*Segmento 2 (120-240 s):*

- Media R-R: 0.8262 s 
  
- SDNN:      0.0809 s (80,9 ms)

## **Interpretación de los resultados:**

En el primer segmento (0–120 s) se obtuvo una SDNN de 132.7 ms, un valor clasificado como excepcional, lo que refleja una excelente variabilidad de la frecuencia cardiaca y una alta capacidad de regulación del sistema nervioso autónomo. Para el segundo segmento (120–240 s), la SDNN fue de 80.9 ms, ubicándose dentro del rango saludable. Esto indica que, aunque la variabilidad cardiaca disminuyó en la segunda parte de la señal, aún se mantiene dentro de niveles fisiológicamente adecuados. 

# **Parte C**
##**Construcción del diagrama de Poincaré**

<pre>
import numpy as np
import matplotlib.pyplot as plt

# Cargar intervalos RR de los dos segmentos
RR1 = np.loadtxt("intervalos_RR_segmento1.txt")   # Reposo
RR2 = np.loadtxt("intervalos_RR_segmento2.txt")   # Lectura

# FUNCIONES PARA SD1, SD2, CVI, CSI

def calcular_SD1_SD2(RR):
    diffRR = np.diff(RR) # diferencias entre RR(n+1) - RR(n)
    SD1 = np.sqrt((np.std(diffRR)**2) / 2)
    SD2 = np.sqrt(2*(np.std(RR)**2) - SD1**2)
    return SD1, SD2

def calcular_CVI_CSI(SD1, SD2):
    CVI = np.log10(SD1 * SD2)
    CSI = SD2 / SD1
    return CVI, CSI

# Calcular parámetros para cada segmento
SD1_1, SD2_1 = calcular_SD1_SD2(RR1)
SD1_2, SD2_2 = calcular_SD1_SD2(RR2)

CVI_1, CSI_1 = calcular_CVI_CSI(SD1_1, SD2_1)
CVI_2, CSI_2 = calcular_CVI_CSI(SD1_2, SD2_2)

# DIAGRAMA DE POINCARÉ
def grafica_poincare(RR, titulo):
    RR_n = RR[:-1]
    RR_n1 = RR[1:]

    plt.figure(figsize=(6,6))
    plt.scatter(RR_n, RR_n1, alpha=0.6)
    plt.title(titulo)
    plt.xlabel("RR(n) [s]")
    plt.ylabel("RR(n+1) [s]")
    plt.grid(True)
    plt.show()

# Gráficas
grafica_poincare(RR1, "Diagrama de Poincaré – Reposo (0–120 s)")
grafica_poincare(RR2, "Diagrama de Poincaré – Lectura (120–240 s)")

# MOSTRAR RESULTADOS
print("RESULTADOS DEL POINCARÉ")
print("Reposo:")
print(f"SD1 = {SD1_1:.4f}  (actividad parasimpática)")
print(f"SD2 = {SD2_1:.4f}  (actividad simpática)")
print(f"CVI = {CVI_1:.4f}")
print(f"CSI = {CSI_1:.4f}")
print()
print("Lectura:")
print(f"SD1 = {SD1_2:.4f}  (actividad parasimpática)")
print(f"SD2 = {SD2_2:.4f}  (actividad simpática)")
print(f"CVI = {CVI_2:.4f}")
print(f"CSI = {CSI_2:.4f}")

  </pre>

## **Diagramas de Poincaré - Lectura**

<img width="538" height="548" alt="image" src="https://github.com/user-attachments/assets/d0893e11-9abc-4ed6-9c4a-a178709597ae" />

## **Diagramas de Poincaré - Lectura**

<img width="545" height="548" alt="image" src="https://github.com/user-attachments/assets/e81306d8-5e4e-4c17-9afb-57ec4e0f6874" />

## **RESULTADOS DEL POINCARÉ**

**Reposo:**
SD1 = 0.0996  (actividad parasimpática)
SD2 = 0.1591  (actividad simpática)
CVI = -1.8001
CSI = 1.5977

**Lectura:**
SD1 = 0.0522  (actividad parasimpática)
SD2 = 0.1019  (actividad simpática)
CVI = -2.2745
CSI = 1.9526


# **Conclusiones**

# **Bibiografia**
[1] “Sistema Nervioso Simpático y Parasimpático: Anatomía y Funciones Clave - Fisioterapia y Rehabilitación”. fisioterapos.com - Blog de Información. Accedido el 14 de noviembre de 2025. [En línea]. Disponible: https://fisioterapos.com/sistema-nervioso-simpatico-y-parasimpatico-anatomia/

[2] H. medicus, “Estimulación simpática y parasimpática en el corazón,” Homo medicus, Sep. 14, 2025. https://homomedicus.com/efecto-de-la-estimulacion-simpatica-y-parasimpatica-sobre-la-frecuencia-cardiaca/ (accessed Nov. 14, 2025)

[3] “Variabilidad de la frecuencia cardiaca como factor predictor de las enfermedades cardiovasculares”. Elsevier | Un negocio de análisis de información. Accedido el 14 de noviembre de 2025. [En línea]. Disponible: https://www.elsevier.es/es-revista-revista-colombiana-cardiologia-203-articulo-variabilidad-frecuencia-cardiaca-como-factor-S0120563319300683

[4] G. Escudero Prieto, “Procesamiento digital de la señal para el diagnóstico precoz de la Enfermedad de Parkinson,” 1library.com, Feb. 01, 2016. https://1library.co/document/z3dkjjp7-procesamiento-diagn%C3%B3stico-enfermedad-parkinson-caracterizaci%C3%B3n-espectral-variabilidad-card%C3%ADaco.html (accessed Nov. 17, 2025).

[5] M. M. Corrales, B. de la C. Torres, A. G. Esquivel, M. A. G. Salazar, and J. Naranjo Orellana, “Normal values of heart rate variability at rest in a young, healthy and active Mexican population,” Health, vol. 04, no. 07, pp. 377–385, 2012, doi: https://doi.org/10.4236/health.2012.47060.

[6] “Heart rate variability (HRV) - What is normal HRV range,” Kubios, Sep. 23, 2024. https://www.kubios.com/blog/heart-rate-variability-normal-range/
‌
