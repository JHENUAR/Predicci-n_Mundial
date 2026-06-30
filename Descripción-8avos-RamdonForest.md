# Predicción de Clasificados a Octavos de Final – Mundial 2026

## 🏆 Descripción del proyecto

Este proyecto utiliza técnicas de Machine Learning para predecir los ganadores de los dieciseisavos de final del Mundial 2026, determinando así los 16 equipos que avanzarán a octavos de final. Se emplea un modelo Random Forest entrenado con más de 2.000 partidos históricos, combinado con estadísticas actualizadas de los equipos (ranking FIFA, valor de mercado, rendimiento en fase de grupos) y una estimación de goles esperados mediante distribución de Poisson.

El proyecto está concebido como un trabajo universitario que demuestra la integración de técnicas de aprendizaje automático, análisis de datos y simulación estocástica en el dominio deportivo.

---

## 🎯 Objetivos

### Primario

Determinar qué equipos superan la ronda de dieciseisavos y se clasifican a octavos de final.

### Secundarios

* Estimar los goles esperados para cada enfrentamiento.
* Cuantificar la incertidumbre de la predicción mediante simulación Monte Carlo.
* Generar un flujo de trabajo reproducible y documentado.

---

## 📊 Datos utilizados

### Fuentes

| Archivo              | Descripción                                                                                                             | Procedencia               |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------- | ------------------------- |
| cruces_16avos.csv    | Emparejamientos de dieciseisavos de final (16 partidos).                                                                | Página oficial de la FIFA |
| datos_historicos.csv | Historial de partidos internacionales con estadísticas detalladas (goles, xG, posesión, tiros, tarjetas, faltas, etc.). | Recopilación propia       |
| datos_mundial.csv    | Estadísticas agregadas por equipo durante la fase de grupos del Mundial 2026.                                           | Informes oficiales FIFA   |
| ranking_fifa.csv     | Puntuación ELO de cada equipo según ranking FIFA.                                                                       | FIFA World Ranking        |
| transfermarkt.csv    | Valor de mercado de la plantilla (millones de euros).                                                                   | Transfermarkt             |

---

## 📁 Estructura de los datos

Cada archivo contiene columnas específicas:

### datos_historicos

* Equipo_Local
* Equipo_Visitante
* Goles_Local
* Goles_Visitante
* avg_Goles_esperados_(xG)_total_Local
* avg_Posesión_total_Local
* avg_Remates_a_puerta_total_Local

### datos_mundial

* Puntos
* avg_Goles_total
* avg_Posesión_total
* avg_Remates_a_puerta_total

### ranking_fifa

* Equipo
* Puntuación

### transfermarkt

* Equipo
* Valor_Mercado_Millones_Eur

---

## 🔄 Normalización de nombres

| Nombre original                 | Nombre normalizado |
| ------------------------------- | ------------------ |
| Estados Unidos                  | EE. UU.            |
| Bosnia y Herzegovina            | Bosnia-Herzegovina |
| República Democrática del Congo | RD Congo           |
| Côte d'Ivoire                   | Costa de Marfil    |

---

## 💾 Almacenamiento y acceso

Los datos están en Google Drive:

```python
from google.colab import drive
drive.mount('/content/drive')
```

```python
base_path = '/content/drive/MyDrive/Simulaciones_Mundial/Data'
```

---

## 🧹 Preprocesamiento

Se realiza limpieza y normalización de nombres para evitar errores de coincidencia entre datasets.

---

## 🧠 Metodología y modelo

### 1. Construcción del dataset

Se calculan diferencias entre estadísticas del equipo local y visitante.

Variable objetivo:

* 1 → victoria local
* 0 → empate
* -1 → victoria visitante

---

### 2. Modelo Random Forest

* Árboles: 500
* Profundidad máxima: 12
* random_state: 42

Validación:

* 5-fold estratificado
* Precisión: ~60–65%

---

### 3. Estimación de goles (Poisson)

[
\lambda_{home} = \max(0.1,; \overline{goles}*{home} \cdot (0.8 + 0.4 \cdot p*{home}))
]

[
\lambda_{away} = \max(0.1,; \overline{goles}*{away} \cdot (0.8 + 0.4 \cdot p*{away}))
]

---

### 4. Simulación Monte Carlo

* 1000 iteraciones
* Distribución de Poisson
* Penales en caso de empate
* Basado en ranking FIFA

---

### 5. Implementación técnica

Librerías:

* pandas
* numpy
* scikit-learn
* re
* warnings

---

## 🔧 Instalación

```bash
pip install pandas numpy scikit-learn
```

---

## 🚀 Ejecución

### Google Colab

1. Abrir Colab
2. Montar Drive
3. Ajustar base_path
4. Ejecutar

---

### Entorno local

```bash
python prediccion_octavos.py
```

---

## 📈 Resultados esperados
* Marcador más probable.

* Probabilidades de victoria local, empate y victoria visitante.
* Ganador (clasificado a octavos).

* Lista de clasificados – los 16 equipos que avanzan a octavos de final.

* Porcentajes de clasificación – calculados mediante Monte Carlo, indicando la frecuencia con que cada equipo supera la ronda.
---

### Tabla de predicciones

Incluye:

* Equipos
* xG
* Marcador
* Probabilidades
* Ganador

### Ejemplo

| Local     | Visitante | xG_Local | xG_Visitante | Goles Local | Goles Visitante | Prob Local | Prob Empate | Prob Visitante | Ganador   |
| --------- | --------- | -------- | ------------ | ----------- | --------------- | ---------- | ----------- | -------------- | --------- |
| Sudáfrica | Canadá    | 1.45     | 1.12         | 1           | 1               | 0.42       | 0.28        | 0.30           | Sudáfrica |
| Alemania  | Paraguay  | 2.34     | 0.58         | 2           | 1               | 0.68       | 0.18        | 0.14           | Alemania  |

---

### Salidas

* Tabla de predicciones
* Lista de clasificados
* Porcentajes Monte Carlo

---

## 📝 Notas importantes

* Si algún equipo no aparece en los archivos de estadísticas, se le asignan valores por defecto (cero) para que el modelo pueda ejecutarse sin errores.

* Los datos de ranking FIFA y valor de mercado deben estar actualizados para obtener predicciones precisas.

* La simulación Monte Carlo utiliza una semilla aleatoria fija (random_state=42) para garantizar la reproducibilidad.

---

## 🧪 Validación

* Validación cruzada
* Código modular
* Semilla fija

---

## 🔗 Enlaces

* https://www.fifa.com/en/tournaments/mens/worldcup/canadamexicousa2026/standings
* https://www.transfermarkt.es/
* https://scikit-learn.org/

Referencia:
Maher, M. J. (1982). *Modelling association football scores*. Statistica Neerlandica.

---

## 👨‍💻 Autor

Proyecto desarrollado como trabajo académico en análisis de datos y Machine Learning aplicado al deporte.

