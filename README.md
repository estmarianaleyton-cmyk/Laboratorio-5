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

**- Aumenta mucho la fuerza de contracción de toda la musculatura cardíaca, tanto auricular como ventricular.** [2]



## ***Variabilidad de la frecuencia cardíaca (HRV) obtenida a partir de la señal electrocardiográfica (ECG)***

La variabilidad de la frecuencia cardíaca (HRV) es un reflejo directo de la modulación del sistema nervioso autónomo sobre el corazón. El aumento del tono parasimpático incrementa la variabilidad entre los intervalos R-R en el ECG, mientras que la activación simpática disminuye dicha variabilidad al generar una respuesta cronotrópica positiva. Por lo tanto, la HRV es un indicador sensible del equilibrio simpático-parasimpático y permite evaluar la función autonómica cardíaca en condiciones de reposo, estrés o actividad física. El análisis de la HRV obtenido del ECG es una herramienta fundamental en la fisiología cardiovascular, ya que permite inferir el estado autonómico y predecir alteraciones del sistema cardiovascular asociadas a predominio simpático, como la hipertensión, la dislipidemia, la diabetes o el sedentarismo.[3]

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

## **Código en Python (Google colab)**

# **Parte C**

# **Conclusiones**

# **Bibiografia**
[1]“Sistema Nervioso Simpático y Parasimpático: Anatomía y Funciones Clave - Fisioterapia y Rehabilitación”. fisioterapos.com - Blog de Información. Accedido el 14 de noviembre de 2025. [En línea]. Disponible: https://fisioterapos.com/sistema-nervioso-simpatico-y-parasimpatico-anatomia/

[2] H. medicus, “Estimulación simpática y parasimpática en el corazón,” Homo medicus, Sep. 14, 2025. https://homomedicus.com/efecto-de-la-estimulacion-simpatica-y-parasimpatica-sobre-la-frecuencia-cardiaca/ (accessed Nov. 14, 2025)

‌
[3]“Variabilidad de la frecuencia cardiaca como factor predictor de las enfermedades cardiovasculares”. Elsevier | Un negocio de análisis de información. Accedido el 14 de noviembre de 2025. [En línea]. Disponible: https://www.elsevier.es/es-revista-revista-colombiana-cardiologia-203-articulo-variabilidad-frecuencia-cardiaca-como-factor-S0120563319300683

[4]G. Escudero Prieto, “Procesamiento digital de la señal para el diagnóstico precoz de la Enfermedad de Parkinson,” 1library.com, Feb. 01, 2016. https://1library.co/document/z3dkjjp7-procesamiento-diagn%C3%B3stico-enfermedad-parkinson-caracterizaci%C3%B3n-espectral-variabilidad-card%C3%ADaco.html (accessed Nov. 17, 2025).
‌
