# 📊 Comparativa de Modelos de Machine Learning para la Predicción de Resultados en el Mundial 2026

---

## 📌 Introducción

En el presente trabajo se han desarrollado y evaluado **dos modelos de clasificación** para predecir los ganadores de los dieciseisavos de final del Mundial de Fútbol 2026, con el objetivo de determinar los **16 equipos que avanzarán a octavos de final**.

Ambos modelos utilizan características basadas en estadísticas históricas y actuales:

* Ranking FIFA
* Valor de mercado
* Rendimiento en fase de grupos
* Estadísticas de juego (xG, posesión, tiros, etc.)

### 🔍 Modelos evaluados

* 🌲 **Random Forest Classifier** (primer enfoque)
* ⚡ **XGBoost Classifier** (segundo enfoque con optimización e híbrido)

---

## 🌲 Modelo 1: Random Forest

### 📖 Descripción

Random Forest es un algoritmo de *ensemble learning* que construye múltiples árboles de decisión y combina sus predicciones mediante votación.

---

### ⚙️ Configuración

* Árboles: 500
* Profundidad máxima: 12
* Criterio: Gini
* Random state: 42

---

### 🏋️ Entrenamiento

* +2000 partidos históricos
* +30 variables (diferencias entre equipos)
* Variable objetivo:

  * `1` → Local
  * `0` → Empate
  * `-1` → Visitante
* Validación: **Stratified 5-Fold**

---

### 📈 Rendimiento

| Métrica           | Valor    |
| ----------------- | -------- |
| Precisión (CV)    | 61–63 %  |
| Precisión (train) | 68–70 %  |
| Tiempo            | Moderado |

---

### ✅ Ventajas

* Alta interpretabilidad
* Robusto a ruido y outliers
* Buen rendimiento sin mucho ajuste

---

### ❌ Desventajas

* Limitado en relaciones complejas
* Menor precisión en patrones no lineales

---

## ⚡ Modelo 2: XGBoost

### 📖 Descripción

XGBoost utiliza *gradient boosting*, construyendo árboles secuenciales donde cada uno corrige errores del anterior.

---

### ⚙️ Configuración

* Árboles: 300
* Profundidad: 8
* Learning rate: 0.05
* Subsample: 0.8
* Colsample: 0.8
* Métrica: `mlogloss`
* Random state: 42

---

### 🏋️ Entrenamiento

* Mismos datos que Random Forest

* Features mejoradas:

  * Ratio goles/posesión
  * Ratio tarjetas/faltas

* Validación: 5-Fold

* Optimización: Grid Search

---

## ⚖️ Enfoque híbrido (clave del proyecto)

* Si probabilidad > 60 % → ganador directo
* Si no → simulación con Poisson (1000 iteraciones)

✔ Mejora decisiones en partidos inciertos
✔ Genera resultados más realistas

---

### 📈 Rendimiento

| Métrica           | Valor |
| ----------------- | ----- |
| Precisión (CV)    | 66 %  |
| Precisión (train) | 78 %  |
| Tiempo            | Alto  |

---

### ✅ Ventajas

* Mayor precisión
* Captura relaciones complejas
* Regularización (reduce overfitting)
* Ajuste fino de hiperparámetros
* Enfoque híbrido mejora decisiones

---

### ❌ Desventajas

* Sensible a hiperparámetros
* Mayor costo computacional
* Menor interpretabilidad

---

## 📊 Comparativa general

| Aspecto              | Random Forest | XGBoost        |
| -------------------- | ------------- | -------------- |
| Tipo                 | Bagging       | Boosting       |
| Precisión CV         | 61–63 %       | 66 %           |
| Precisión train      | 68–70 %       | 78 %           |
| Sobreajuste          | Bajo          | Controlado     |
| Tiempo               | Medio         | Alto           |
| Interpretabilidad    | Alta          | Media          |
| Relaciones complejas | Bueno         | Excelente      |
| Decisión             | Votación      | Prob + Poisson |

---

## 🔬 Conclusión

Ambos modelos logran resultados sólidos considerando la **naturaleza impredecible del fútbol**.

Sin embargo, **XGBoost supera a Random Forest** en precisión y capacidad predictiva.

---

### 🏆 ¿Por qué XGBoost?

* Mayor precisión
* Mejor modelado de relaciones complejas
* Enfoque híbrido reduce errores en partidos cerrados
* Regularización efectiva
* Alta flexibilidad

---

## ⚠️ Limitaciones

* Precisión máxima ~66 %
* Falta de variables clave:

  * Lesiones
  * Clima
  * Motivación

---

## 🚀 Trabajo futuro

* Incorporar datos más detallados
* Usar redes neuronales
* Ensemble de modelos
* Optimizar umbral del enfoque híbrido

---

## 🏁 Conclusión final

El modelo **XGBoost con enfoque híbrido (Poisson + ML)** es la mejor solución para este proyecto, ofreciendo:

* Mayor precisión
* Mayor robustez
* Mejor toma de decisiones en incertidumbre

---

## 📚 Referencias

* Chen, T., & Guestrin, C. (2016). *XGBoost: A Scalable Tree Boosting System*.
* Breiman, L. (2001). *Random Forests*.
* Maher, M. J. (1982). *Modelling association football scores*.
* Pedregosa et al. (2011). *Scikit-learn*.
* FIFA World Cup: https://www.fifa.com/
