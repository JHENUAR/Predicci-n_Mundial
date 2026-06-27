# 🌍⚽ World Cup Knockout Stage Predictor

### 🧠 Predicción de equipos clasificados a Octavos de Final usando Machine Learning

---

## 🚀 Descripción del Proyecto

Este proyecto implementa un modelo de **Machine Learning supervisado** para predecir:

* ⚽ Resultados de partidos (goles por equipo)
* 🏆 Equipos clasificados a Octavos de Final
* 📊 Comportamiento competitivo entre selecciones

El sistema simula enfrentamientos reales del torneo utilizando datos históricos, rankings y métricas de rendimiento.

---

## 🎯 Objetivo

Construir un modelo capaz de:

✔ Estimar el resultado de partidos eliminatorios
✔ Identificar el equipo ganador
✔ Simular automáticamente una fase completa del torneo
✔ Analizar qué variables influyen más en el resultado

---

## 🧠 Modelo Utilizado

### 🔹 Random Forest Regressor

Se utiliza el modelo:

```python
RandomForestRegressor(n_estimators=100, random_state=42)
```

### 📌 ¿Por qué Random Forest?

* Maneja relaciones no lineales
* Reduce overfitting mediante múltiples árboles
* Funciona bien con datos heterogéneos
* No requiere escalamiento estricto

---

## ⚙️ Pipeline del Modelo

El flujo completo del sistema es:

```text
1. Carga de datos
2. Limpieza y normalización
3. Integración de datasets
4. Feature Engineering
5. Entrenamiento del modelo
6. Predicción de goles
7. Simulación de partidos
8. Determinación de clasificados
```

---

## 📊 Ingeniería de Características (Feature Engineering)

El modelo no usa valores absolutos, sino **diferencias entre equipos**:

```python
df["ranking_diff"] = df["ranking_team1"] - df["ranking_team2"]
df["value_diff"] = df["value_team1"] - df["value_team2"]
df["form_diff"] = df["form_team1"] - df["form_team2"]
```

### 🔥 Variables clave:

* Ranking FIFA 🌍
* Valor de plantilla 💰
* Forma reciente 📈
* Historial competitivo 🏆
* Promedio de goles ⚽

👉 Esto permite que el modelo entienda quién es “más fuerte” en cada partido.

---

## 📂 Estructura del Proyecto

```text
📦 world-cup-predictor
 ┣ 📂 data
 ┃ ┣ partidos.csv
 ┃ ┣ ranking_fifa.csv
 ┃ ┣ transfermarkt.csv
 ┃ ┣ datos_historicos.csv
 ┃ ┣ datos_mundial.csv
 ┃ ┣ detalle_simulacion_torneo.csv
 ┃ ┗ cruces_16avos.csv
 ┃
 ┣ 📂 notebooks
 ┃ ┗ analisis_exploratorio.ipynb
 ┃
 ┣ 📂 src
 ┃ ┣ preprocessing.py
 ┃ ┣ feature_engineering.py
 ┃ ┣ model.py
 ┃ ┗ simulation.py
 ┃
 ┣ 📂 results
 ┃ ┗ predicciones.csv
 ┃
 ┣ main.py
 ┗ README.md
```

---

## 🧪 Entrenamiento del Modelo

```python
X = df[features]
y = df[["goles_team1", "goles_team2"]]

model = RandomForestRegressor()
model.fit(X, y)
```

---

## ⚽ Predicción de Partidos

Para cada cruce:

```python
pred = model.predict(nuevo_partido)
```

Salida:

```text
Equipo A 2 - 1 Equipo B
👉 Clasificado: Equipo A
```

---

## 🏆 Simulación del Torneo

El sistema:

1. Lee los cruces (`cruces_16avos.csv`)
2. Predice cada partido
3. Determina el ganador
4. Genera automáticamente los clasificados

---

## 📈 Resultados Esperados

* Predicciones realistas de marcadores
* Clasificación coherente según datos históricos
* Identificación de favoritos

---

## ⚠️ Problemas Comunes (y solución)

### ❌ Error: `KeyError: 'team'`

✔ Causa: el dataset no contiene la columna `"team"`
✔ Solución:

```python
print(df.columns)
```

Y usar el nombre correcto, por ejemplo:

```python
df["Team"]  # o df["equipo"]
```

---

## 📊 Posibles Mejoras

* 🔥 XGBoost / LightGBM
* 📉 Feature importance visualization
* 🌐 Dashboard interactivo (Streamlit)
* 🧠 Optimización de hiperparámetros
* 🏆 Simulación completa del Mundial

---

## 🛠️ Tecnologías

* Python
* Pandas
* NumPy
* Scikit-learn

---

## 💡 Conclusión

Este proyecto demuestra cómo aplicar Machine Learning para:

* Modelar competencias deportivas
* Simular escenarios complejos
* Generar predicciones basadas en datos reales

---
