# Analisis de la Oferta Inmobiliaria Urbana
### Analisis Multivariado con R: PCA + Clustering + MCA

## 🔗 Ver reporte en línea

[![Ver en RPubs](https://img.shields.io/badge/RPubs-Ver%20Reporte-blue)](https://rpubs.com/MBExcel/1397259)

👉 [Análisis completo publicado en RPubs](https://rpubs.com/MBExcel/1397259)

![R](https://img.shields.io/badge/R-4.x-blue)
![RMarkdown](https://img.shields.io/badge/RMarkdown-Reporte-lightgrey)
![FactoMineR](https://img.shields.io/badge/FactoMineR-PCA_Clustering-green)
![Status](https://img.shields.io/badge/Estado-Completo-green)

---

## Problema

Una empresa inmobiliaria requiere comprender en profundidad el mercado de viviendas urbanas para tomar decisiones estrategicas informadas. A partir de una base de datos con informacion detallada sobre propiedades residenciales, se realiza un analisis holistico para identificar patrones, relaciones y segmentaciones que permitan mejorar la toma de decisiones en compra, venta y valoracion de propiedades.

---

## Dataset

- **Fuente:** `paqueteMODELOS` — dataset `vivienda` (mercado inmobiliario urbano colombiano)
- **Registros:** 8.319 viviendas tras depuracion
- **Variables:** atributos fisicos, socioeconomicos y espaciales

| Variable | Tipo | Descripcion |
|----------|------|-------------|
| preciom | Numerica | Precio del inmueble |
| areaconst | Numerica | Area construida (m2) |
| habitaciones | Numerica | Numero de habitaciones |
| banos | Numerica | Numero de banos |
| parqueaderos | Categorica | Numero de parqueaderos |
| estrato | Numerica/Factor | Estrato socioeconomico (1-6) |
| tipo | Factor | Tipo de vivienda (casa/apartamento) |
| zona | Factor | Zona geografica |
| barrio | Factor | Barrio |
| latitud / longitud | Numerica | Coordenadas geograficas |

---

## Pipeline del Analisis

```
Carga de datos (paqueteMODELOS::vivienda)
        │
        ▼
Analisis Exploratorio (EDA)
  - Tipo de datos y estadisticas descriptivas
  - Valores faltantes por variable
  - Matriz de correlaciones de Pearson
  - Histograma de precios
  - Boxplots: precio vs habitaciones, precio vs estrato
  - Scatter: precio vs area por tipo de vivienda
  - Mapa geografico: precio por ubicacion y estrato
        │
        ▼
Transformacion de datos
  - Eliminacion de registros sin informacion suficiente
  - Conversion de variables a factor
  - Imputacion de faltantes categoricos como "No informado"
        │
        ▼
Analisis de Componentes Principales (PCA)
  - Libreria: FactoMineR
  - Variables cuantitativas activas + variables cualitativas suplementarias
  - Circulo de correlaciones
  - Varianza explicada por componente (Scree Plot)
  - Contribuciones individuales Dim 1 y Dim 2
        │
        ▼
Analisis de Conglomerados (Clustering)
  - Metodo: HCPC (Hierarchical Clustering on Principal Components)
  - Numero de clusters determinado automaticamente por ganancia de inercia
  - Descripcion de clusters por variables cuantitativas
        │
        ▼
Analisis de Correspondencias Multiples (MCA)
  - Variables: zona, tipo y estrato
  - Biplot factorial de categorias
        │
        ▼
Conclusiones y Recomendaciones estrategicas
```

---

## Tecnicas Estadisticas Aplicadas

| Tecnica | Libreria | Uso |
|---------|----------|-----|
| Analisis de Componentes Principales | FactoMineR | Reduccion de dimensionalidad |
| Clustering Jerarquico (HCPC) | FactoMineR | Segmentacion del mercado |
| Analisis de Correspondencias Multiples | FactoMineR | Relacion entre variables categoricas |
| Matriz de correlaciones | corrplot | Identificacion de variables relacionadas |
| Visualizacion multivariada | factoextra | Graficos de PCA y clusters |

---

## Segmentos del Mercado Identificados

| Cluster | Perfil | Caracteristicas | Estrategia |
|---------|--------|-----------------|------------|
| **1** | Economico | Menor area, menos banos, estratos bajos, precio bajo | Proyectos de volumen |
| **2** | Medio | Tamano y precio moderado, perfil familiar | Priorizar — mayor liquidez |
| **3** | Premium | Mayor area, mas servicios, estratos altos, precio alto | Rentabilidad y exclusividad |

---

## Hallazgos Clave

- El **82.5%** de la varianza se explica con los dos primeros componentes principales
- Las variables mas influyentes en el precio son: **area construida, banos y parqueaderos** (correlacion ~70% con preciom)
- Las viviendas de **mayor precio** se concentran en el sur, oriente y occidente de la ciudad
- Los **estratos 5 y 6** presentan los precios mas altos con mayor variabilidad
- Las mujeres mas jovenes (dato del MCA) revelan que **apartamentos** → zona sur, estratos 4-5; **casas** → zona norte/centro, estratos medios-bajos
- La **zona oeste** se asocia con estrato 6 y viviendas de alto valor

---

## Visualizaciones incluidas

- Histograma de precios con distribucion
- Boxplot: precio vs habitaciones
- Boxplot: precio vs estrato
- Scatter: precio vs area construida por tipo de vivienda
- Mapa geografico: precio por latitud/longitud y estrato
- Circulo de correlaciones PCA
- Grafico de varianza explicada (Scree Plot)
- Contribuciones individuales Dim 1 y Dim 2
- Grafico de clusters (fviz_cluster)
- Biplot MCA: zona, tipo y estrato
- Tabla interactiva del dataset depurado (DT::datatable)

---

## Stack Tecnologico

```r
paqueteMODELOS   # Dataset vivienda
tidyverse        # Manipulacion y transformacion de datos
ggplot2          # Visualizaciones estadisticas
FactoMineR       # PCA, HCPC, MCA
factoextra       # Visualizacion de resultados multivariados
corrplot         # Matriz de correlaciones
knitr + kableExtra  # Tablas profesionales en HTML
DT               # Tabla interactiva del dataset
```

---

## Como reproducir el analisis

```r
# 1. Instalar dependencias
install.packages(c("tidyverse", "ggplot2", "FactoMineR", "factoextra",
                   "corrplot", "knitr", "kableExtra", "DT"))

# Instalar paqueteMODELOS desde repositorio
# devtools::install_github("dgonxalex80/paqueteMODELOS")

# 2. Abrir el archivo .Rmd en R Studio
# 3. Hacer clic en "Knit" para generar el reporte HTML
```

> **Nota:** Las imagenes `Imagen_cali.avif` y `registro eliminados.PNG` deben estar
> en la misma carpeta que el archivo .Rmd para que el reporte se genere correctamente.

---

## Ver el reporte

El reporte HTML con todos los resultados, graficos interactivos y tablas paginadas
esta disponible en el archivo `Actividad_1-Evaluacion_oferta_inmobiliaria.html`
incluido en este repositorio.

---

## Estructura del repositorio

```
analisis-mercado-inmobiliario-R/
│
├── Actividad_1-Evaluacion_oferta_inmobiliaria_final.Rmd   # Codigo fuente
├── Actividad_1-Evaluacion_oferta_inmobiliaria_final.html  # Reporte renderizado
├── Imagen_cali.avif                                        # Imagen encabezado
├── registro eliminados.PNG                                 # Imagen referenciada
└── README.md
```

---

## Autor

**Oscar Mauricio Montano**
Analista de Datos | Power BI · SQL · Python · R | Maestrante en Ciencia de Datos

mbexcel@hotmail.com · Portafolio: https://github.com/msorin81
