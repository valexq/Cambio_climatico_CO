# Proyecto de Analítica de Datos y Modelo Predictivo — Cambio Climático Colombia

Análisis integral del sistema ENSO (El Niño / La Niña) entre 1950 y 2026, aplicando
un flujo ETL → EDA → Dashboard de BI → Modelos predictivos supervisados,
con énfasis en el impacto del fenómeno sobre Colombia.

---

## Dataset

- **Nombre:** `Cambio climatico`
- **Fuente:** [Indicador de Cambio Climático — datos.gov.co (IDEAM)](https://www.datos.gov.co/dataset/Cambio-clim-tico/bgt6-7zyr/about_data)
- **Registros:** 916 registros mensuales (1950–2026), 914 tras limpieza
- **Variables:** 17 columnas tras transformación (temperatura, anomalías, fase, intensidad, duración y variables derivadas)

## Diccionario de variables

| Campo | Descripción | Unidad |
|---|---|---|
| `Fecha` | Fecha mensual del registro | YYYY-MM-DD |
| `Anio` | Año del registro | YYYY |
| `Mes` | Mes del registro (1–12) | Número |
| `Trimestre` | Trimestre del año (1–4) | Número |
| `Decada` | Década del registro (1950s–2020s) | Texto |
| `Temperatura_Pacifico_C` | Temperatura superficial del mar en la región Niño 3.4 del Pacífico ecuatorial | °C |
| `Temperatura_Base_C` | Temperatura climatológica de referencia mensual (línea base histórica) | °C |
| `Anomalia_C` | Desviación mensual respecto a la temperatura base | °C |
| `ONI_C` | Índice ONI — promedio hacia adelante de 3 meses consecutivos de `Anomalia_C` | °C |
| `ONI_Round` | Índice ONI redondeado a 1 decimal | °C |
| `Anomalia_12m` | Promedio móvil de 12 meses de la anomalía mensual | °C |
| `Anomalia_Delta` | Cambio mensual de la anomalía respecto al mes anterior | °C |
| `Fase_ONI` | Fase ENSO según el ONI trimestral: El Nino / La Nina / Neutral | Texto |
| `Fase_Evento` | Fase ENSO del evento activo en ese mes | Texto |
| `Intensidad_Evento` | Clasificación NOAA: Débil / Moderado / Fuerte / Muy Fuerte / Neutral | Texto |
| `Duracion_Meses` | Meses consecutivos del evento activo en la misma fase | Meses |
| `Evento_Extremo` | Indicador binario: 1 si \|ONI_C\| ≥ 1.5°C | 0/1 |

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

El dataset contiene 914 registros mensuales del sistema ENSO entre 1950 y 2026,
con variables como temperatura del Pacífico, anomalía térmica, índice ONI, fase del evento,
intensidad y duración. A partir de ellos se construye una solución analítica que cubre
limpieza de datos, análisis exploratorio, modelo de BI y modelado predictivo supervisado.

---

## Objetivos

Desarrollar un proyecto integral sobre el sistema ENSO con énfasis en su impacto en Colombia:

- Datos limpios y transformados listos para análisis.
- Dashboard de BI con KPIs e insights sobre el ciclo ENSO.
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
│   │   └── Cambio_climatico.csv          # Dataset crudo ENSO (916 registros)
│   ├── cleaned/
│   │   └── enso_cleaned.csv              # Dataset limpio (914 filas, 8 cols)
│   └── processed/
│       └── enso_model_ready.csv          # Dataset con variables derivadas (914 filas, 17 cols)
│
├── notebooks/
│   ├── 01_etl.ipynb                      #  limpieza y transformación 
│   ├── 02_eda.ipynb                      #  análisis exploratorio 
│   ├── 03_modelos_pred.ipynb             # modelos predictivos 
│
├── reports/
│   ├── eda_01_distribuciones.png
│   ├── eda_02_boxplots_fase.png
│   ├── eda_03_categoricas.png
│   ├── eda_04_serie_temporal.png
│   ├── eda_05_intensidad_decada.png
│   ├── eda_06_estacionalidad.png
│   ├── eda_07_correlaciones.png
│   ├── eda_08_scatter.png
│   ├── eda_09_episodios_colombia.png
│   └── eda_10_temperatura_anual.png
│   └── eda_11_duracion_intensidad.png
│   └── eda_12_delta.png
│
├── requirements.txt
└── README.md
```

---

## Fase 1 - ETL: extracción, transformación y carga 

Se trabajó con el archivo crudo `data/raw/Cambio_climatico.csv`, que contiene
916 registros mensuales de temperaturas y anomalías del Pacífico ecuatorial entre
1950 y 2026, publicado por el IDEAM en datos.gov.co.

El trabajo de esta fase se concentró en dejar una base confiable para el análisis.
Se renombraron columnas al español, se estandarizaron las categorías de fase ENSO,
se eliminaron 2 registros con ONI incompleto (marzo y abril 2026, cuyos meses futuros
no existen aún) y se construyeron 9 variables derivadas clave.

| Variable derivada | Descripción |
|---|---|
| `Anio`, `Mes`, `Trimestre`, `Decada` | Componentes temporales extraídos de la fecha |
| `Intensidad_Evento` | Clasificación NOAA por magnitud del ONI trimestral |
| `Duracion_Meses` | Meses consecutivos del evento activo en la misma fase |
| `Evento_Extremo` | 1 si \|ONI_C\| ≥ 1.5°C |
| `Anomalia_12m` | Promedio móvil de 12 meses de la anomalía |
| `Anomalia_Delta` | Cambio mensual de la anomalía |

> **Decisión metodológica:** la intensidad del evento se clasifica con el **ONI trimestral**
> (`ONI_C`), no con la anomalía mensual puntual, conforme al estándar internacional de la NOAA.

**Resultado:** `enso_cleaned.csv` (914 filas, 8 columnas) y `enso_model_ready.csv` (914 filas, 17 columnas).

---

## Fase 2 - EDA: análisis exploratorio de datos 

Se tomó el dataset procesado y se realizó una exploración en 14 secciones para
entender el comportamiento del sistema ENSO y su relación con Colombia.
Se revisaron distribuciones, boxplots por fase, tendencias por década, estacionalidad
mensual, correlaciones y los episodios históricos más críticos.

### Hallazgos principales del EDA

1. Los eventos de El Niño se han **intensificado desde la década de 1980**, con
   mayor frecuencia de anomalías superiores a ±1.5°C en los 1990s y 2010s.
2. Colombia se ve afectada en años de El Niño fuerte (1982–83, 1997–98, 2015–16)
   con sequías, y en años de La Niña intensa (1999–2000, 2010–11) con inundaciones.
3. El **El Niño 2015–16** registró la anomalía más alta del periodo histórico (+2.77°C).
4. La **La Niña 2010–11** fue el episodio más devastador para Colombia por inundaciones,
   con 3.2 millones de damnificados.
5. Los meses de **septiembre a noviembre** son los más críticos para Colombia: el pico
   estacional del ENSO coincide con la segunda temporada de lluvias del país.
6. La correlación entre `Anomalia_C` y `ONI_C` es de r = 0.98, y entre `ONI_C` y
   `Anomalia_12m` es de r = 0.96, confirmando la coherencia interna del dataset.

---

## Fase 3 — Inteligencia de Negocios: modelo de datos y dashboard 



## Fase 4 — Modelado predictivo



