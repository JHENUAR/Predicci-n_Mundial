# 🏆 Modelo de Predicción de Partidos - Copa del Mundo

## 🚀 Descripción del Proyecto

Este proyecto implementa un modelo de **Machine Learning** para predecir los resultados de partidos de fútbol en fases eliminatorias de la Copa del Mundo.

El sistema combina información estadística de múltiples fuentes para estimar:

* 📊 Probabilidades de victoria (local, empate, visitante)
* ⚽ Marcadores simulados usando distribución de Poisson
* 🏆 Equipos clasificados a la siguiente fase

---

## 🧠 Enfoque del Modelo

El modelo utiliza un enfoque basado en:

### 🔹 1. Ingeniería de características

Se calculan diferencias estadísticas entre equipos:

* Ranking FIFA
* Valor de mercado (Transfermarkt)
* Rendimiento en torneos

Ejemplo:

```python
match[f"{col}_diff"] = s_h[col] - s_a[col]
```

---

### 🔹 2. Modelo de Machine Learning

Se utiliza un modelo:

```python
RandomForestClassifier
```

Configuración:

```python
model = RandomForestClassifier(
    n_estimators=500,
    max_depth=12,
    random_state=42
)
```

---

### 🔹 3. Escalado de datos

```python
scaler = StandardScaler()
X_scaled = scaler.fit_transform(X)
```

---

### 🔹 4. Predicción de probabilidades

El modelo predice:

* 🟢 Victoria local → `1`
* ⚪ Empate → `0`
* 🔴 Victoria visitante → `-1`

---

### 🔹 5. Simulación de marcador (Poisson)

Para estimar goles:

```python
lam_home = 1.2 + (p_home * 2)
lam_away = 1.2 + (p_away * 2)

goles_home = np.random.poisson(lam_home)
goles_away = np.random.poisson(lam_away)
```

---

## 📂 Estructura del Proyecto

```
📁 proyecto-mundial
│
├── 📄 modelo.py
├── 📄 README.md
├── 📄 requirements.txt
│
├── 📁 data/
│   ├── cruces_16avos.csv
│   ├── datos_historicos.csv
│   ├── datos_mundial.csv
│   ├── ranking_fifa.csv
│   ├── transfermarkt.csv
│   └── ...
```
---

📂 Datos Utilizados

El modelo utiliza múltiples fuentes de datos para construir las variables predictivas. A continuación se describen los datasets empleados:

📊 Archivos principales

Los datos deben almacenarse en la carpeta data/ con la siguiente estructura:
```
data/
├── cruces_16avos.csv
├── datos_historicos.csv
├── datos_mundial.csv
├── ranking_fifa.csv
├── transfermarkt.csv
├── partidos.csv
├── partidos_mundial.csv
├── Grupos_Mundial.csv
└── detalle_simulacion_torneo.csv
```
---

📌 Descripción de los datasets
* cruces_16avos.csv
Contiene los enfrentamientos de la fase eliminatoria.
* datos_historicos.csv
Resultados de partidos históricos entre selecciones (goles, local/visitante).
* datos_mundial.csv
Estadísticas de desempeño en torneos internacionales.
* ranking_fifa.csv
Ranking oficial de selecciones nacionales.
* transfermarkt.csv
Valor de mercado de los equipos o jugadores.
* partidos.csv / partidos_mundial.csv
Información detallada de partidos jugados.
* Grupos_Mundial.csv
Distribución de equipos por grupos.
* detalle_simulacion_torneo.csv
Datos adicionales para simulación del torneo.

---

## ⚠️ Consideraciones

* El modelo depende de la calidad de los datos
* La simulación de Poisson introduce aleatoriedad
* Los resultados son probabilísticos, no deterministas

---

## 🚀 Mejoras futuras

* 📊 Visualización de resultados (gráficas)
* 🤖 Modelos más avanzados (XGBoost, Deep Learning)
* 🌎 API para predicciones en tiempo real
* 📈 Evaluación del modelo (accuracy, F1-score)

---


## ⭐ Conclusión

Este proyecto demuestra cómo combinar:

* Machine Learning
* Estadística
* Simulación probabilística

para generar predicciones realistas en el ámbito deportivo, siendo una excelente base para proyectos de análisis avanzado y portafolio profesional.
