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

El filtro se diseñó con la función butter de SciPy utilizando la representación en coeficientes directos (b y a) tras normalizar los bordes de banda respecto a la frecuencia de Nyquist (0.5·fs). Luego se verificó que el coeficiente a [0] fuera igual a 1 y, de no ser así, se normalizaron los arreglos para cumplir la forma estándar de la ecuación en diferencias. Finalmente, la señal se filtró, acumulando las contribuciones de muestras actuales y pasadas (parte numérica) y restando las contribuciones de salidas anteriores (parte recursiva), obteniendo así una señal ECG limpia dentro del intervalo útil de 0.5–40 Hz.

## **Division de la señal en dos segmentos y calculos de los intervalos de los picos R-R:**

## **Código en Python (Google colab)**
<pre> ```
señ_filt = np.loadtxt(filename)
N = len(señ_filt)
t = np.arange(N) / fs
duracion_total = N / fs
print(f"Duración total: {duracion_total:.2f} s ({duracion_total/60:.2f} min)")


  
</pre>




# **Parte C**

# **Conclusiones**

# **Bibiografia**
[1]“Sistema Nervioso Simpático y Parasimpático: Anatomía y Funciones Clave - Fisioterapia y Rehabilitación”. fisioterapos.com - Blog de Información. Accedido el 14 de noviembre de 2025. [En línea]. Disponible: https://fisioterapos.com/sistema-nervioso-simpatico-y-parasimpatico-anatomia/

[2] H. medicus, “Estimulación simpática y parasimpática en el corazón,” Homo medicus, Sep. 14, 2025. https://homomedicus.com/efecto-de-la-estimulacion-simpatica-y-parasimpatica-sobre-la-frecuencia-cardiaca/ (accessed Nov. 14, 2025)

‌
[3]“Variabilidad de la frecuencia cardiaca como factor predictor de las enfermedades cardiovasculares”. Elsevier | Un negocio de análisis de información. Accedido el 14 de noviembre de 2025. [En línea]. Disponible: https://www.elsevier.es/es-revista-revista-colombiana-cardiologia-203-articulo-variabilidad-frecuencia-cardiaca-como-factor-S0120563319300683

[4]G. Escudero Prieto, “Procesamiento digital de la señal para el diagnóstico precoz de la Enfermedad de Parkinson,” 1library.com, Feb. 01, 2016. https://1library.co/document/z3dkjjp7-procesamiento-diagn%C3%B3stico-enfermedad-parkinson-caracterizaci%C3%B3n-espectral-variabilidad-card%C3%ADaco.html (accessed Nov. 17, 2025).
‌
