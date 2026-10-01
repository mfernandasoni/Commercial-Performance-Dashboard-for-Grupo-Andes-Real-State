# Real Estate Commercial Performance Dashboard for Grupo Andes

🌐 [English](#english) | [Español](#español)

---

<a name="english"></a>
## 🇬🇧 English

A Power BI executive dashboard analyzing sales, customers, and properties to support data-driven strategic decisions.

### 1. Context / Problem
This was an individual project developed as part of the **TripleTen Data Analyst certificate program**. The real estate sector needed to evaluate its commercial performance — growth, profitability, and customer behavior — for Grupo Andes. The request was to build an executive dashboard covering sales, customers, and properties, working from four source tables: a sales transaction fact table (`hecho_ventas_propiedades`) and three dimension tables (`dim_clientes`, `dim_propiedades`, and a calendar table, `dim_fecha`, to be built as part of the modeling).

The dashboard needed to answer four groups of business questions: general performance (total revenue, number of sales, average sale price, total commission), commercial analysis (which property type, customer segment, and sales channel generate the most revenue), temporal analysis (sales trend, year-over-year growth, YTD performance), and customer cohorts (whether customers repurchase, and which cohorts generate more revenue over time).

### 2. My Contribution
I was responsible for the full process: data cleaning, building the calendar table, modeling the star schema, creating all DAX measures, structuring the report, and writing the executive summary.

### 3. Process and Decisions
- **Data cleaning:** I validated data types (dates, numeric fields, `porcentaje_comision` as a percentage), checked for null values and justified whether to keep or remove them, and validated that the primary keys in `dim_clientes` and `dim_propiedades` had no duplicates — ensuring the model would be built on reliable data.
- **Calendar table (`dim_fecha`):** I built it with DAX's `CALENDAR` and `ADDCOLUMNS` functions, with the date range generated dynamically from the minimum to the maximum `fecha_venta` in the fact table, rather than hardcoding a fixed range — so the table stays correct if the underlying data changes. I included Year, Month name, Month number, and Year-Month columns to support flexible time-based analysis.
- **Star schema modeling:** I connected `hecho_ventas_propiedades` as the central fact table to the three dimension tables, with one-to-many cardinality, single filter direction, and all relationships active and built on the correct keys — a structure chosen to keep the model simple to filter and performant.
- **Measure design in three tiers:** I separated measures by purpose rather than building them ad hoc:
  - **Base measures** (Total Revenue, Number of Sales, Average Ticket, Total Commission) for the headline KPIs.
  - **Filter-context measures** using `CALCULATE` to compute revenue share (%) by property type, sales channel, and customer segment — removing the category filter from the denominator while keeping it in the numerator, so these could be used as tooltips that show each category's contribution to the whole.
  - **Time intelligence measures** (YTD and YoY growth, built from `dim_fecha`) to track the business's evolution over time.
  - **Cohort calculated columns** (first purchase date, cohort month, sale month) built directly on the fact table, since cohort analysis required row-level values rather than aggregated measures — these feed the cohort matrix.
- **Three-page report structure:** I organized the dashboard into an Executive Overview (KPIs, sales trend, revenue by city, YoY growth), a Commercial Analysis page (revenue by property type/channel/segment, with a conditionally formatted table highlighting top performers), and a Cohort Analysis page (a cohort matrix with cohort month as rows, sale month as columns, and sales/revenue as values) — mirroring the three groups of business questions the dashboard needed to answer.

### 4. Outcome / Learning
- Total revenue for the period (Jan 2023–Dec 2024) was **USD 6,012.5 million**, from **8,500 sales**, with an average ticket of **USD 707,353** and total commission of **USD 200,627,166**.
- **Casa** (house) generates the most revenue (USD 2,240.5 M) despite **Departamento** (apartment) having the highest sales volume (5,105 sales) — Casa's average ticket (USD 964,086) is far higher than Departamento's (USD 361,856).
- **Mexico City** is the top-revenue city (USD 3,242.2 M / 4,123 sales), slightly ahead of **Bogotá** (USD 2,770.3 M / 4,377 sales) — Bogotá sells more units but at a lower average value.
- The **Corredor** (broker) channel is by far the most efficient, generating 73% of total revenue (USD 4,380.0 M) versus USD 1,632.5 M from the Direct channel.
- The **First-Time** customer segment drives most of the revenue (63%, USD 3,783.6 M, 5,302 sales), while the smaller **Investor** and **High Net Worth** segments contribute less volume but, in the case of High Net Worth, the highest value per transaction.
- The 2023-02 cohort showed the highest repurchase rate (93.0%), and overall sales grew **+11.1% YoY** (2023: USD 2,847.7 M → 2024: USD 3,164.8 M).
- Delivered strategic recommendations: prioritize higher-ticket property types (Casa and Comercial), strengthen and incentivize the Corredor channel while evaluating ways to scale Direct sales, build retention strategies targeted at First-Time buyers, and plan campaigns around the YoY seasonality pattern.

### 5. Tools Used
- Power BI (Power Query, DAX: `CALENDAR`, `ADDCOLUMNS`, `CALCULATE`, time intelligence functions)

### 6. Evidence
- 📊 Power BI file (.pbix): see repository
- 📓 Project notebook (English version) with the full process and executive summary: see repository

---

# Estrategia comercial de Andes Capital Real Estate

<a name="español"></a>
## 🇪🇸 Español

Un dashboard ejecutivo en Power BI que analiza ventas, clientes y propiedades para apoyar decisiones estratégicas basadas en datos.

### 1. Contexto / Problema
Este fue un proyecto individual desarrollado como parte del **certificado de Data Analyst de TripleTen**. El sector inmobiliario necesitaba evaluar su desempeño comercial —crecimiento, rentabilidad y comportamiento de clientes— para Grupo Andes. Se solicitó construir un dashboard ejecutivo que cubriera ventas, clientes y propiedades, a partir de cuatro tablas fuente: una tabla de hechos de transacciones de venta (`hecho_ventas_propiedades`) y tres tablas dimensionales (`dim_clientes`, `dim_propiedades`, y una tabla calendario, `dim_fecha`, que debía construirse como parte del modelado).

El dashboard debía responder cuatro grupos de preguntas de negocio: desempeño general (ingreso total, cantidad de ventas, precio promedio de venta, comisión total), análisis comercial (qué tipo de propiedad, segmento de cliente y canal de venta generan más ingresos), análisis temporal (tendencia de ventas, crecimiento año contra año, desempeño YTD) y cohortes de clientes (si los clientes recompran y qué cohortes generan más ingresos con el tiempo).

### 2. Mi Contribución
Fui responsable de todo el proceso: limpieza de datos, construcción de la tabla calendario, modelado del esquema estrella, creación de todas las medidas DAX, estructuración del reporte y elaboración del resumen ejecutivo.

### 3. Proceso y Decisiones
- **Limpieza de datos:** Validé los tipos de datos (fechas, campos numéricos, `porcentaje_comision` como porcentaje), revisé valores nulos y justifiqué si debían eliminarse o mantenerse, y validé que las claves primarias de `dim_clientes` y `dim_propiedades` no tuvieran duplicados, asegurando que el modelo se construyera sobre datos confiables.
- **Tabla calendario (`dim_fecha`):** La construí con las funciones DAX `CALENDAR` y `ADDCOLUMNS`, con el rango de fechas generado dinámicamente desde la fecha mínima hasta la máxima de `fecha_venta` en la tabla de hechos, en lugar de un rango fijo, para que la tabla se mantenga correcta si los datos subyacentes cambian. Incluí columnas de Año, Mes (nombre), Número de mes y Año-Mes para soportar análisis temporales flexibles.
- **Modelado en esquema estrella:** Conecté `hecho_ventas_propiedades` como tabla de hechos central a las tres tablas dimensionales, con cardinalidad uno a muchos, dirección de filtro simple, y todas las relaciones activas y construidas sobre las claves correctas, una estructura elegida para mantener el modelo simple de filtrar y con buen rendimiento.
- **Diseño de medidas en tres niveles:** Separé las medidas por propósito en lugar de crearlas de forma improvisada:
  - **Medidas base** (Ingreso Total, Cantidad de Ventas, Ticket Promedio, Comisión Total) para los KPIs principales.
  - **Medidas con contexto de filtro** usando `CALCULATE` para calcular la participación (%) de ingresos por tipo de propiedad, canal de venta y segmento de cliente, eliminando el filtro de la dimensión en el denominador mientras se mantiene en el numerador, para poder usarlas como tooltips que muestran la contribución de cada categoría al total.
  - **Medidas de inteligencia de tiempo** (YTD y crecimiento YoY, construidas a partir de `dim_fecha`) para monitorear la evolución del negocio en el tiempo.
  - **Columnas calculadas de cohortes** (fecha de primera compra, mes cohorte, mes de venta) construidas directamente en la tabla de hechos, ya que el análisis de cohortes requería valores a nivel de fila en lugar de medidas agregadas; estas alimentan la matriz de cohortes.
- **Estructura del reporte en tres páginas:** Organicé el dashboard en un Overview Ejecutivo (KPIs, tendencia de ventas, ingresos por ciudad, crecimiento YoY), una página de Análisis Comercial (ingresos por tipo de propiedad/canal/segmento, con una tabla de formato condicional que resalta a los de mejor desempeño), y una página de Análisis de Cohortes (una matriz de cohortes con mes cohorte en filas, mes de venta en columnas, y ventas/ingresos como valores), reflejando los tres grupos de preguntas de negocio que el dashboard debía responder.

### 4. Resultado / Aprendizaje
- El ingreso total del periodo (ene 2023–dic 2024) fue de **USD 6,012.5 millones**, a partir de **8,500 ventas**, con un ticket promedio de **USD 707,353** y una comisión total de **USD 200,627,166**.
- **Casa** genera el mayor ingreso (USD 2,240.5 M) a pesar de que **Departamento** tiene el mayor volumen de ventas (5,105 ventas); el ticket promedio de Casa (USD 964,086) es mucho mayor que el de Departamento (USD 361,856).
- **Ciudad de México** es la ciudad con mayor ingreso (USD 3,242.2 M / 4,123 ventas), levemente por encima de **Bogotá** (USD 2,770.3 M / 4,377 ventas); Bogotá vende más unidades pero a menor valor promedio.
- El canal **Corredor** es por lejos el más eficiente, generando el 73% del ingreso total (USD 4,380.0 M) frente a USD 1,632.5 M del canal Directo.
- El segmento de clientes **Primera vez** impulsa la mayor parte del ingreso (63%, USD 3,783.6 M, 5,302 ventas), mientras que los segmentos más pequeños **Inversionista** y **Alto patrimonio** aportan menor volumen, aunque Alto patrimonio tiene el mayor valor por transacción.
- La cohorte de 2023-02 mostró la mayor tasa de recompra (93.0%), y las ventas totales crecieron **+11.1% YoY** (2023: USD 2,847.7 M → 2024: USD 3,164.8 M).
- Se entregaron recomendaciones estratégicas: priorizar tipos de propiedad de mayor ticket (Casa y Comercial), fortalecer e incentivar el canal Corredor mientras se evalúan formas de escalar las ventas Directas, construir estrategias de retención dirigidas a compradores Primera vez, y planificar campañas en torno al patrón de estacionalidad detectado en el crecimiento YoY.

### 5. Herramientas Utilizadas
- Power BI (Power Query, DAX: `CALENDAR`, `ADDCOLUMNS`, `CALCULATE`, funciones de inteligencia de tiempo)

### 6. Evidencias
- 📊 Archivo de Power BI (.pbix): ver repositorio
- 📓 Notebook del proyecto (versión en español) con el proceso completo y el resumen ejecutivo: ver repositorio
