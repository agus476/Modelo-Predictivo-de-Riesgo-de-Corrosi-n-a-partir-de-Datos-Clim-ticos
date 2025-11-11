# Modelo Predictivo de Riesgo de Corrosión a partir de Datos Climáticos

Este repositorio contiene un prototipo de modelo de **riesgo de corrosión ambiental** construido a partir de datos reales de clima obtenidos desde la API de **OpenWeather**.  

El objetivo no es modelar corrosión física real, sino mostrar un **pipeline completo de IA aplicada**:

1. Ingesta de datos desde una API externa.
2. Construcción de un dataset enriquecido con features de calendario y un índice sintético de contaminación.
3. Simulación de una tasa de corrosión (`corrosion_rate`) coherente con las condiciones ambientales.
4. Exploración visual (EDA).
5. Entrenamiento y evaluación de modelos de regresión (Linear Regression vs Random Forest).
6. Visualización de resultados (real vs predicho).

> En un entorno real, la columna `corrosion_rate` se reemplazaría por mediciones industriales de corrosión, inspecciones o indicadores de integridad de activos.

---

## 🧠 Contexto

El prototipo está pensado para escenarios de:

- **Mantenimiento predictivo** en activos expuestos al ambiente (estructuras metálicas, cañerías, equipos).
- **Análisis de riesgo ambiental** según clima y posible presencia de contaminantes.
- Integración futura con dashboards (Power BI, Power Apps) o flujos de automatización (Power Automate, Zapier, Make).

---

## 🏗️ Arquitectura del notebook

El flujo principal está implementado en el notebook:

`notebooks/Modelo_Predictivo_de_Riesgo_de_Corrosión_a_partir_de_Datos_Climáticos.ipynb`

Secciones principales:

1. **Configuración e ingesta de datos**
   - Lectura de la API key de OpenWeather.
   - Llamada al endpoint de pronóstico 5-day / 3-hour.
   - Normalización de la respuesta JSON en un `DataFrame` con variables climáticas clave.

2. **Construcción del dataset de corrosión**
   - Features de calendario: `hour`, `dayofweek`.
   - Encoding cíclico de la hora: `hour_sin`, `hour_cos`.
   - Índice sintético de contaminación (`pollution_index`) basado en:
     - dirección del viento (`wind_deg`),
     - velocidad del viento (`wind_speed`),
     - su alineación con una “zona industrial” hipotética.
   - Simulación de `corrosion_rate` como combinación de:
     - humedad, viento, nubosidad, temperatura y contaminación,
     - más un término de ruido aleatorio controlado.

3. **Exploración visual (EDA)**
   - Serie temporal de `corrosion_rate`.
   - Relación temperatura vs corrosión (color = contaminación).
   - Distribución de corrosión por hora del día (boxplot).
   - Menú interactivo para elegir el gráfico a visualizar.

4. **Modelado**
   - Definición de `X` (features climáticas + calendarización + contaminación) y `y` (`corrosion_rate`).
   - Split temporal 70% / 30% (train / test).
   - Entrenamiento de:
     - `LinearRegression`,
     - `RandomForestRegressor`.

5. **Evaluación**
   - Métricas en test:
     - **MAE** (Mean Absolute Error),
     - **R²** (coeficiente de determinación).
   - Gráficos de desempeño:
     - Corrosión real vs predicha (serie temporal).
     - Gráfico de dispersión real vs predicho con línea ideal `y = x`.

6. **Conclusiones y próximos pasos**
   - Discusión sobre qué tan bien captura el modelo la dinámica simulada.
   - Cómo se reemplazaría la corrosión simulada por datos reales.
   - Posibles integraciones en un entorno industrial.

---

## ⚙️ Requisitos

- Python 3.9+ recomendado.
- Librerías indicadas en `requirements.txt`:
## 📓 Notebook online (Google Colab)

También podés explorar el proyecto directamente en Google Colab:

[👉 Abrir en Google Colab](https://colab.research.google.com/drive/1MIxN09-qUOJqyDIQVDhGXzheKHAElmSE)




## 🔑 Configuración de la API de OpenWeather

Este proyecto utiliza el endpoint de pronóstico **5-day/3-hour** de [OpenWeather](https://openweathermap.org/forecast5).

1. Crear una cuenta en OpenWeather y obtener una **API key**.
2. Configurar la variable de entorno `OPENWEATHER_API_KEY` en tu sistema, por ejemplo:

**Linux / macOS (bash/zsh):**


## 🚀 Cómo ejecutar el proyecto localmente

# Clonar el repositorio:

- git clone https://github.com/tu-usuario/corrosion-risk-demo.git
- cd corrosion-risk-demo


(Opcional, pero recomendado) Crear un entorno virtual:

python -m venv .venv
source .venv/bin/activate   # Linux/macOS
# .venv\Scripts\activate    # Windows


# Instalar dependencias:

- pip install -r requirements.txt


#Configurar la variable de entorno OPENWEATHER_API_KEY (ver sección anterior).

# Abrir el notebook:

- jupyter notebook notebooks/Modelo_Predictivo_de_Riesgo_de_Corrosión_a_partir_de_Datos_Climáticos.ipynb




## 📈 Próximos pasos posibles

- Reemplazar la corrosión simulada por:

- mediciones reales de corrosión,

- registros de inspecciones,

- indicadores de integridad de equipos.

- Agregar más fuentes de datos:

- calidad de aire (SO₂, NOₓ, partículas),

- proximidad a zonas industriales o rutas,

- datos de operación (paradas, cambios de proceso, etc.).

- Exponer el modelo como:

- API interna,

- dashboard (Power BI, Streamlit, etc.),


- componente de un flujo de automatización (Power Automate, Zapier, Make).
