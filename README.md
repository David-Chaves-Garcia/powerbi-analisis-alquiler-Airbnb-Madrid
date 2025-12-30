# powerbi-analisis-alquiler-Airbnb-Madrid
## Power BI informe analítico de la estructura, disponibilidad y comportamiento del mercado del alquiler de Airbnb en Madrid

### 📊 Análisis del mercado Airbnb en Madrid
Proyecto de Power BI

### 🎯 Objetivo del proyecto
El objetivo de este proyecto es analizar la estructura del mercado de Airbnb en Madrid desde una perspectiva económica y de uso real, poniendo el foco en:  
· La variabilidad espacial (distritos y barrios)  
· Los patrones de disponibilidad y uso  
· El grado de concentración de la oferta en manos de grandes anfitriones


El informe está orientado principalmente a:  
· inversores inmobiliarios  
· analistas de mercado y urbanismo  
· propietarios que quieren entender la estructura competitiva del mercado


### 🧾 Dataset y preparación de datos
El dataset ha sido obtenido de Inside Airbnb. Dataset listings.csv Madrid, Comunidad de Madrid, Spain. 14 Septiembre de 2025
El dataset original presenta:  
· una proporción relevante de valores nulos, especialmente en precios y disponibilidad  
· outliers extremos en precios  
· estructuras no normalizadas para análisis agregado


Decisiones clave de limpieza:  
· Se eliminaron aproximadamente el 25 % de los registros sin precio, documentado explícitamente.  
· Los outliers no se eliminaron, ya que forman parte del mercado real; se trataron únicamente a nivel visual.  


### 🧱 Modelado de datos
El modelo sigue un esquema en estrella, con relaciones 1:* activas y correctas.  
#### Tabla de hechos  
Fact_Listado: precios, disponibilidad, identificadores de alojamiento y propietario, etc.  
#### Tablas de dimensión  
Dim_Propietario  
Dim_Alojamiento (tipo de alojamiento)  
Dim_Ubicacion (distrito y barrio)  
#### Tabla intermedia  
Tramos Concentración

Este modelado permite:  
· análisis agregados robustos  
· uso correcto de medidas  
· navegación coherente entre dimensiones

### 📄 Estructura del informe
El informe se organiza en cuatro páginas, siguiendo una narrativa analítica progresiva.

### 1️⃣ Distribución de precios
![Distribución de precios](images/pagina_1_precios.png)
Pregunta clave:  
¿Cómo es la estructura de precios del mercado Airbnb en Madrid?

Visuales principales:  
#### KPIs:  
- Precio mediano
- Percentil 25
- Percentil 75
- Precio medio


#### Histograma de precios:
- bins de 25 €  
- eje truncado en el percentil 95 para mejorar legibilidad  
- nota aclaratoria indicando que los valores extremos se mantienen en el análisis  

#### Decisiones analíticas:
- Se prioriza la mediana frente a la media debido a la fuerte presencia de outliers.  
- El IQR se interpreta siempre en relación con la mediana, no como valor aislado.  

### 2️⃣ Estructura espacial de precios
Pregunta clave:  
¿Cómo varían los precios según la ubicación?  
Visuales:  
- Precio mediano por distrito  
- Precio mediano por barrio  
Interacción:  
- El gráfico de distritos actúa como selector que filtra barrios.  
- No se utiliza segmentador de distrito para evitar redundancia.  
Esta página permite identificar:  
- diferencias inter-distrito  
- alta variabilidad intra-distrito en algunos casos  
- Valores extremos de precio mediano por barrio en algunos casos debido a que cuenta con muy pocos valores y son justamente extremos

### 3️⃣ Disponibilidad y patrones de uso
Pregunta clave:  
¿Cómo se utilizan realmente los alojamientos a lo largo del año?  
Visuales:  
- Distribución número de alojamientos según disponibilidad  
- Gráfico de anillos % de alojamientos por tramo de disponibilidad  
    · Uso intensivo (0–90 días)  
    · Uso mixto (91–180)  
    · Uso ocasional (181–300)  
    · Prácticamente siempre disponible (301–365)
- Scatter de relación entre disponibilidad media y precio mediano por tipo de alojamiento

   
KPIs:  
- Disponibilidad media  
- Percentil 25 de disponibilidad  
- Percentil 75 de disponibilidad  
- % de alojamientos disponibles 365 días  


Decisiones analíticas:
- Se utiliza media para disponibilidad (distribución menos extrema que precios).  
- Los percentiles 25 y 75 permiten identificar el rango típico de uso, excluyendo comportamientos extremos.  
- El binning se implementa mediante columnas calculadas, no medidas, para garantizar estabilidad y orden correcto.  

### 4️⃣ Concentración del mercado
Pregunta clave:  
¿Está la oferta distribuida de forma atomizada o concentrada?  
Visuales:  
- Barra apilada:  
% de alojamientos gestionados por:  
· Top 1 % de anfitriones  
· Siguiente 4 %  
· Siguiente 5 %  
· Resto (90 %)  

- Gráfico de barras:  
. Distribución de anfitriones según número de alojamientos (1, 2–3, 4–10, >10)
  

KPIs:  
- Total de propietarios  
- Total de alojamientos  
- Media de alojamientos por propietario  
- % de alojamientos en manos del top 10 %


Esta página muestra de forma clara que:  
· existe una alta concentración de la oferta   
· una minoría de anfitriones gestiona una proporción muy significativa del mercado

### 🔗 Navegación y experiencia de usuario
· Menú lateral izquierdo persistente en todas las páginas.  
· Indicador visual de página activa mediante barra de color.  
· Botones contextuales que permiten profundizar manteniendo filtros.  
· Segmentadores sincronizados entre páginas cuando es relevante. 


#### 🛈 Uso de tooltips explicativos
El informe incorpora tooltips contextuales en los principales visuales y KPIs para facilitar su interpretación.
Estos tooltips explican conceptos estadísticos clave (percentiles, dispersión, concentración) y criterios analíticos,
permitiendo mantener el diseño limpio sin sobrecargar las páginas con texto visible.  

El diseño prioriza:  
· legibilidad  
· coherencia visual  
· mínima fricción cognitiva  

### 🧠 Principales conclusiones
==> El mercado presenta una distribución de precios altamente asimétrica, donde la media no es representativa.  
==> La ubicación explica parte del precio, pero existe una variabilidad relevante dentro de los mismos distritos.  
==> La disponibilidad muestra patrones heterogéneos, reflejando distintos modelos de uso (residencial, mixto, inversión).  

La oferta está claramente concentrada en un pequeño porcentaje de anfitriones, lo que tiene implicaciones económicas y regulatorias.

### 🛠️ Herramientas utilizadas

Power BI Desktop  
DAX para medidas y columnas calculadas
