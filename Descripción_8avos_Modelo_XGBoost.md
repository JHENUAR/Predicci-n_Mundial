# 🚀 Predicción de Clasificados a Octavos de Final – Mundial 2026 - MODELO XGBOOST

---

## 📌 Descripción del proyecto

Este proyecto aplica técnicas de **Machine Learning** para predecir los ganadores de los dieciseisavos de final del Mundial de Fútbol 2026, determinando así los 16 equipos que avanzarán a octavos de final.

El modelo utiliza un enfoque híbrido que combina:

- 🌳 Un clasificador **XGBoost** entrenado con más de 2.000 partidos internacionales históricos.
- 📊 Probabilidades de:
  - Victoria local
  - Empate
  - Victoria visitante
- 🎲 Un mecanismo de desempate basado en la **distribución de Poisson**.
- 🔁 Simulación **Monte Carlo (1000 iteraciones)** para medir la incertidumbre.

Este proyecto está diseñado como trabajo universitario integrando:
- Machine Learning
- Análisis de datos
- Simulación estocástica

---

## 🎯 Objetivos

### 🥇 Objetivo principal
Determinar qué equipos se clasifican a **octavos de final**.

### 📌 Objetivos secundarios
- Estimar goles esperados (**xG**)
- Cuantificar incertidumbre (Monte Carlo)
- Generar un flujo reproducible

---

## 📊 Datos utilizados

### 📁 Archivos necesarios

| Archivo | Descripción | Procedencia |
|--------|------------|------------|
| `cruces_16avos.csv` | Emparejamientos | FIFA |
| `datos_historicos.csv` | +2000 partidos históricos | Bases públicas |
| `datos_mundial.csv` | Estadísticas del Mundial 2026 | FIFA |
| `ranking_fifa.csv` | Ranking ELO | FIFA |
| `transfermarkt.csv` | Valor de mercado | Transfermarkt |

📌 Ubicación esperada:
```bash
/content/drive/MyDrive/Simulaciones_Mundial/Data
