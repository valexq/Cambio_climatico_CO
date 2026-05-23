# Proyecto de Analítica de Datos y Modelo Predictivo — Cambio Climático Colombia

Análisis del fenómeno ENOS (El Niño / La Niña) y su relación con variables climatológicas,
eventos de salud pública y desastres en Colombia (2007–2025), aplicando un flujo
ETL → EDA → Dashboard de BI → Modelos predictivos supervisados.

---

## Dataset

- **Nombre:** Cambio climático
- **Fuente:** [Indicador de Cambio Climático — datos.gov.co (IDEAM / Ministerio de Salud)](https://www.datos.gov.co/dataset/Cambio-clim-tico/bgt6-7zyr/about_data)
- **Última actualización:** 6 de abril de 2026
- **Registros:** 228 registros mensuales (2007–2025), 204 con datos completos de salud (desde 2009)
- **Variables:** 33 columnas 
- 
## Diccionario de variables

| Campo | Descripción | Unidad |
|---|---|---|
| `Fecha` | Fecha mensual del registro | YYYY-MM-DD |
| `Anio` | Año del registro | YYYY |
| `Mes_Nombre` | Mes abreviado en español | Texto |
| `Trimestre` | Trimestre del año (1–4) | Número |
| `Decada` | Década del registro (2000s–2020s) | Texto |
| `Num_Mes_Serie` | Número secuencial del mes desde el inicio de la serie | Número |
| `Fase_ENOS` | Fase ENSO del mes: El Nino / La Nina / Neutral | Texto |
| `ENOS_Indice` | Índice ENOS numérico (anomalía temperatura Pacífico) | °C |
| `Clasificacion_ONI` | Clasificación textual del ONI (NIÑA DÉBIL, NIÑO FUERTE, etc.) | Texto |
| `Intensidad_ENOS` | Clasificación NOAA: Débil / Moderado / Fuerte / Muy Fuerte / Neutral | Texto |
| `Evento_Extremo` | Indicador binario: 1 si \|ENOS_Indice\| ≥ 1.5°C | 0/1 |
| `Temperatura_Max_C` | Temperatura máxima mensual registrada | °C |
| `Temperatura_Min_C` | Temperatura mínima mensual registrada | °C |
| `Temperatura_Prom_C` | Temperatura promedio mensual | °C |
| `Temperatura_Prom_12m` | Promedio móvil de 12 meses de la temperatura promedio | °C |
| `Temperatura_Delta` | Variación mensual de la temperatura promedio | °C |
| `Lluvia_Acumulada_mm` | Precipitación acumulada mensual | mm |
| `Lluvia_12m` | Promedio móvil de 12 meses de la lluvia acumulada | mm |
| `Lluvia_Delta` | Variación mensual de la precipitación | mm |
| `Temporada` | Temporada climática: Lluvioso / Menos lluvioso | Texto |
| `Casos_Dengue` | Casos de dengue reportados en el mes | Número |
| `Dengue_Delta` | Variación mensual de casos de dengue | Número |
| `Casos_Leptospirosis` | Casos de leptospirosis reportados | Número |
| `Casos_Respiratorios` | Casos de enfermedades respiratorias (ESI + IRAG) | Número |
| `Eventos_FRM` | Fenómenos de Remoción en Masa (deslizamientos, avalanchas) | Número |
| `Familias_Afectadas` | Familias afectadas por eventos climáticos | Número |
| `Inundaciones` | Número de eventos de inundación | Número |
| `Encharcamientos` | Número de eventos de encharcamiento | Número |
| `Damnificados_Inundaciones` | Personas damnificadas por inundaciones | Número |
| `Damnificados_Encharcamientos` | Personas damnificadas por encharcamientos | Número |
| `Total_Afectados` | Suma de damnificados por inundaciones y encharcamientos | Número |
| `Datos_Completos` | 1 si el registro tiene todos los indicadores (2009+), 0 si es parcial (2007–2008) | 0/1 |
| `Clave_Anio_Mes` | Clave año-mes concatenada (ej. 2009Ene) | Texto |

---

## Integrantes — Grupo 5

| Nombre | Fase principal | GitHub |
|---|---|---|
| Ziuvar Ruiz | Fases 1 y 2 | `@ziuvar` |
| Vanessa Alfaro | Fase 3 | `@valexq` |
| Juan Manuel Valencia | Fases 4 y 5 | `@Juanchos2905` |
| Juan Cardona | Fases 4 y 5 | `@jcardser` |

---

## Descripción del proyecto

El dataset contiene 228 registros mensuales (2007–2025) que cruzan el comportamiento del
fenómeno ENOS con temperatura local, precipitación, casos de dengue, leptospirosis,
enfermedades respiratorias y eventos de desastre en Colombia. A partir de ellos se construye
una solución analítica completa que cubre limpieza de datos, análisis exploratorio,
modelo de BI y modelado predictivo supervisado.

---

## Objetivos

Desarrollar un proyecto integral sobre cambio climático y salud pública en Colombia:

- Datos limpios y transformados listos para análisis.
- Dashboard de BI con KPIs e insights sobre ENOS, clima y salud.
- Modelos supervisados evaluados con métricas de desempeño.
- Conclusiones y recomendaciones basadas en evidencia.

---

## Tecnologías utilizadas

| Componente | Tecnología |
|---|---|
| Lenguaje | Python 3.11 |
| Manipulación de datos | pandas, numpy |
| Visualización | matplotlib, seaborn |
| Machine Learning | scikit-learn |
| Notebooks | Jupyter Notebook |
| Persistencia | CSV |

---

## Arquitectura del proyecto

```text
Cambio_climatico_CO/
│
├── data/
│   ├── raw/
│   │   └── cambioclimatico.csv               # Dataset crudo (228 registros, 2007–2025)
│   ├── cleaned/
│   │   └── cambioclimatico_cleaned.csv       # Dataset limpio (228 filas, 20 cols)
│   └── processed/
│       └── cambioclimatico_model_ready.csv   # Dataset con variables derivadas (228 filas, 33 cols)
│
├── notebooks/
│   ├── 03_etl_cambioclimatico.ipynb          # Extracción, transformación y carga
│   └── 04_eda_cambioclimatico.ipynb          # Análisis exploratorio de datos
│
├── reports/
│   ├── eda_cc_01_distribuciones.png          # Distribuciones de variables numéricas
│   ├── eda_cc_02_boxplots_fase.png           # Variables por fase ENOS
│   ├── eda_cc_03_categoricas.png             # Frecuencia de variables categóricas
│   ├── eda_cc_04_serie_temporal.png          # Evolución temporal 2007–2025
│   ├── eda_cc_05_anuales.png                 # Indicadores anuales
│   ├── eda_cc_06_estacionalidad.png          # Estacionalidad mensual
│   ├── eda_cc_07_correlaciones.png           # Matriz de correlaciones
│   ├── eda_cc_08_scatter.png                 # Relaciones entre variables clave
│   ├── eda_cc_09_episodios.png               # Episodios ENOS críticos
│   └── eda_cc_10_desastres.png               # Impacto social por temporada y fase
│
├── requirements.txt
└── README.md
```

---

## Fase 1 — ETL: extracción, transformación y carga

Se trabajó con el archivo crudo `data/raw/cambioclimatico.csv`, que contiene 228 registros
mensuales de variables climáticas, indicadores de salud pública y eventos de desastre
entre 2007 y 2025, publicado por el IDEAM y el Ministerio de Salud en datos.gov.co.

El trabajo de esta fase se concentró en dejar una base confiable para el análisis.
Se corrigió la codificación de caracteres especiales (ñ en valores de fase ENOS),
se convirtieron columnas numéricas almacenadas con coma decimal, se conservaron las
24 filas de 2007–2008 con indicador de completitud, y se construyeron 10 variables
derivadas clave.

| Variable derivada | Descripción |
|---|---|
| `Trimestre`, `Decada` | Componentes temporales adicionales |
| `Intensidad_ENOS` | Clasificación NOAA: Débil / Moderado / Fuerte / Muy Fuerte |
| `Evento_Extremo` | 1 si \|ENOS_Indice\| ≥ 1.5°C |
| `Temperatura_Prom_12m` | Promedio móvil de 12 meses de la temperatura |
| `Lluvia_12m` | Promedio móvil de 12 meses de la precipitación |
| `Temperatura_Delta` | Variación mensual de temperatura |
| `Lluvia_Delta` | Variación mensual de precipitación |
| `Dengue_Delta` | Variación mensual de casos de dengue |
| `Total_Afectados` | Suma de damnificados por inundaciones y encharcamientos |
| `Datos_Completos` | Indicador binario de completitud del registro |

> **Decisión metodológica:** los registros de 2007–2008 se conservan porque contienen
> datos válidos de temperatura, fase ENOS y desastres, aunque carezcan de indicadores
> de salud. La columna `Datos_Completos` permite filtrar el subconjunto completo cuando
> se requiera.

**Resultado:** `cambioclimatico_cleaned.csv` (228 filas, 20 columnas) y `cambioclimatico_model_ready.csv` (228 filas, 33 columnas).

---

## Fase 2 — EDA: análisis exploratorio de datos

Se tomó el dataset procesado y se realizó una exploración en 14 secciones para
entender el comportamiento del ENOS, las variables climáticas y su relación con la
salud pública y los desastres en Colombia. Se revisaron distribuciones, boxplots por
fase, series temporales, estacionalidad mensual, correlaciones y los episodios
históricos más críticos del periodo 2009–2025.

### Hallazgos principales del EDA

1. El **ENOS tiene un impacto diferenciado** sobre la salud: El Niño aumenta los casos
   de dengue (calor, menos lluvia favorecen al *Aedes aegypti*), mientras que La Niña
   eleva los casos de leptospirosis y respiratorios por el exceso de humedad.
2. La **La Niña 2010–11** fue el evento más devastador del periodo: en un solo mes se
   superaron los 21,000 damnificados y la lluvia acumulada alcanzó niveles históricos.
3. El **El Niño 2015–16** registró el índice ENOS más alto del periodo (+2.5°C),
   con picos de dengue y temperatura por encima del promedio histórico.
4. La lluvia sigue un **patrón bimodal** claramente amplificado por La Niña y reducido
   por El Niño, consistente con el régimen de precipitaciones de Colombia.
5. El dengue y los casos respiratorios tienen **estacionalidad inversa**: el dengue
   sube con el calor (enero–mayo), los respiratorios con el frío y la humedad (mayo–agosto).
6. Las correlaciones más relevantes: `ENOS_Indice` ↔ `Lluvia_Acumulada_mm` (negativa),
   `ENOS_Indice` ↔ `Casos_Dengue` (positiva), `Lluvia` ↔ `Total_Afectados` (positiva).

---

## Fase 3 — Inteligencia de Negocios: modelo de datos y dashboard



## Fase 4 — Modelado predictivo


