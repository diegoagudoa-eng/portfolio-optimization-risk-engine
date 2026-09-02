# Portfolio Optimization & Market Risk Engine (VaR / CVaR & Kupiec Backtesting)

### 📊 Quantitative Portfolio Risk Management & Stress Testing Dashboard

[![Live Demo](https://img.shields.io/badge/LIVE_DEMO-POWER_BI_INTERACTIVE-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://app.powerbi.com/view?r=eyJrIjoiYTI0MTk1Y2EtM2QyZi00MGI3LTliYTMtMzkyMTE5OTI5OWQzIiwidCI6ImY3ZGY1NjA1LWE4OGItNDRkMy05NDFkLWIzMGQ3MjE3M2JjNCIsImMiOjh9)  
[![Python](https://img.shields.io/badge/Python-3.9+-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Quantitative](https://img.shields.io/badge/Quantitative-Risk_Management-EA580C)](#)

> 🚀 **Acceso en vivo:** Explora el cuadro de mando de forma interactiva directamente desde el navegador haciendo clic en la insignia superior o en el siguiente enlace:  
> 👉 **[Ver Dashboard Interactivo en Power BI](https://app.powerbi.com/view?r=eyJrIjoiYTI0MTk1Y2EtM2QyZi00MGI3LTliYTMtMzkyMTE5OTI5OWQzIiwidCI6ImY3ZGY1NjA1LWE4OGItNDRkMy05NDFkLWIzMGQ3MjE3M2JjNCIsImMiOjh9)**

---


Un marco integral en Python para la construcción y optimización de carteras multiactivo (Teoría Moderna de Carteras de Markowitz), la estimación del riesgo de cola mediante tres metodologías complementarias (Value at Risk y Expected Shortfall Paramétrico, Histórico y Monte Carlo) y su posterior validación estadística formal fuera de muestra (Out-of-Sample Backtesting mediante el Test de Kupiec).

---

## 📌 Tabla de Contenidos
1. [Descripción General](#-descripción-general)
2. [Estructura de Activos](#-estructura-de-activos)
3. [Metodología de Optimización y Modelado de Riesgo](#-metodología-de-optimización-y-modelado-de-riesgo)
4. [Resultados Comparativos](#-resultados-comparativos)
5. [Backtesting y Validación Estadística (Test de Kupiec)](#-backtesting-y-validación-estadística-test-de-kupiec)
6. [Conclusiones del Estudio](#-conclusiones-del-estudio)
7. [Limitaciones y Trabajo Futuro](#-limitaciones-y-trabajo-futuro)
8. [Cómo Ejecutar este Proyecto](#-cómo-ejecutar-este-proyecto)

---

## 📖 Descripción General

El proyecto cubre el ciclo analítico cuantitativo completo en gestión de carteras y riesgos:
* Entrenamiento (In-Sample: 2019 – 2024): Descarga automatizada y tratamiento de series temporales de precios ajustados vía `yfinance`, cálculo de rendimientos logarítmicos continuos y optimización de pesos en la frontera eficiente.
* Modelización de Riesgo Extremo: Cuantificación del VaR y CVaR al 99% de confianza para un capital de 1.000.000 USD en un horizonte temporal de 1 día.
* Prueba Fuera de Muestra (Out-of-Sample: 2025 – 2026): Proyección de carteras con pesos fijos sobre cotizaciones no vistas y auditoría empírica mediante la razón de verosimilitud de Kupiec ($LR_{\text{POF}}$).

---

## 📊 Estructura de Activos

El universo está diversificado en 5 ETFs globales de alta liquidez:
* SPY: SPDR S&P 500 ETF Trust (Renta Variable USA - Gran Capitalización).
* VGK: Vanguard FTSE Europe ETF (Renta Variable Europa).
* EMXC: iShares MSCI Emerging Markets ex China ETF (Mercados Emergentes ex-China).
* ASHR: Xtrackers Harvest CSI 300 ETF (Renta Variable China Continental).
* GLD: SPDR Gold Shares (Materias Primas / Refugio).

---

## ⚙️ Metodología de Optimización y Modelado de Riesgo

### 1. Optimización de Carteras (Markowitz)
* Cartera 1/N (Equiponderada): Ponderación fija del 20% por activo ($w_i = 1/5$). Actúa como benchmark de diversificación naive.
* Cartera de Mínima Varianza Global: Minimiza la volatilidad total $\sigma_p = \sqrt{\mathbf{w}^T \boldsymbol{\Sigma} \mathbf{w}}$.
* Cartera de Máximo Ratio de Sharpe: Maximiza el exceso de retorno por unidad de riesgo $(\mu_p - R_f)/\sigma_p$.

## 2. Metodologías de Riesgo de Cola (Confianza 99% / 1 Día / 1.000.000 USD)
* VaR y CVaR Paramétrico (Varianza-Covarianza): Asume distribución normal multivariante: $\text{PnL} \sim \mathcal{N}(\mu_p, \sigma_p^2)$.
* VaR y CVaR Histórico (No Paramétrico): Extrae directamente el percentil 1% empírico de la distribución histórica sin supuestos teóricos.
* Simulación de Monte Carlo: Genera 10.000 escenarios estocásticos de difusión estandarizada: $\text{PnL}_i = V_0 \cdot \mu_p \Delta t + V_0 \cdot \sigma_p \sqrt{\Delta t} \cdot Z_i, \quad Z_i \sim \mathcal{N}(0, 1)$.
---
---

## 📈 Resultados Comparativos

Resumen consolidado de métricas obtenidas sobre un capital de **1.000.000 USD** (Horizonte: 1 día / Confianza: 99%):

| Métrica / Cartera | Cartera 1/N (Equiponderada) | Cartera Mínima Varianza | Cartera Máximo Sharpe |
| :--- | :---: | :---: | :---: |
| **Rentabilidad Anualizada** | 9.11% | 12.35% | 13.40% |
| **Volatilidad Anualizada** | 15.83% | 12.56% | 12.86% |
| **VaR Paramétrico (99%, 1D)** | 23.205 USD | 18.399 USD | 18.847 USD |
| **CVaR Paramétrico (99%, 1D)** | 26.585 USD | 21.080 USD | 21.593 USD |
| **VaR Histórico (99%, 1D)** | 24.785 USD | 21.319 USD | 22.486 USD |
| **CVaR Histórico (99%, 1D)** | 41.990 USD | 29.439 USD | 31.656 USD |
| **VaR Monte Carlo (99%, 1D)** | 22.971 USD | 17.808 USD | 18.127 USD |
| **CVaR Monte Carlo (99%, 1D)** | 27.085 USD | 20.287 USD | 20.848 USD |

---

## 🧪 Backtesting y Validación Estadística (Test de Kupiec)

Para auditar la calibración de los modelos sobre el periodo fuera de muestra ($N = 410$ días, excepciones esperadas: $4.1$), se evalúa la Razón de Verosimilitud de Cobertura Incondicional de Kupiec ($LR_{\text{POF}} \sim \chi^2_1$):

$$LR_{\text{POF}} = -2 \ln \left[ \frac{(1 - p)^{N-x} \, p^x}{\left(1 - \frac{x}{N}\right)^{N-x} \left(\frac{x}{N}\right)^x} \right]$$

### Diagnóstico de Modelos:
* Cartera 1/N (Modelo Validado): Aceptada en los tres métodos ($LR = 2.93$, $\text{p-valor} = 0.0868 > 0.05$). Con 8 excepciones reales ($1.95\%$), la desviación no es estadísticamente suficiente para rechazar el modelo.
* Carteras Optimizadas (Rechazadas): Tanto Mínima Varianza (14 a 24 fallos) como Máximo Sharpe (13 a 19 fallos) son rechazadas ($\text{p-valor} < 0.001$).
* Resiliencia del VaR Histórico: En todas las carteras, el enfoque histórico amortigua sustancialmente mejor las caídas fuera de muestra que los modelos bajo normalidad teórica.

---

## 💡 Conclusiones del Estudio

1. Paradoja de la Optimización y Sobreajuste (Overfitting): El hecho de que la cartera 1/N supere la validación mientras que las óptimas fallen responde a la excesiva dependencia de los datos históricos en el modelo de Markowitz. Durante el periodo de entrenamiento, el oro (GLD) mostró un comportamiento excepcionalmente positivo y baja correlación, provocando una sobreponderación agresiva que perdió eficacia fuera de muestra ante cambios de régimen de mercado. La cartera 1/N, al ser agnóstica a los datos pasados, mostró mayor robustez.
2. Deficiencia del Supuesto de Normalidad: El VaR Paramétrico y Monte Carlo registraron mayor número de rupturas debido a que asumen una distribución gaussiana perfecta. En la práctica, los activos financieros exhiben colas pesadas (fat tails) y asimetría, eventos que el enfoque histórico capta con mayor fidelidad.

---

## 🔍 Limitaciones y Trabajo Futuro

* Modelos Dinámicos de Volatilidad: Implementar modelos GARCH(1,1) para capturar el agrupamiento de volatilidad (volatility clustering) en lugar de considerar varianzas estáticas.
* Distribuciones Asimétricas: Sustituir la normal teórica en Monte Carlo por distribuciones $t$-Student o Cópulas multivariantes.


---

## 🚀 Cómo Ejecutar este Proyecto

1. Clonar el repositorio:
   ```bash
   git clone [https://github.com/diegoagudoa-eng/portfolio-optimization-risk-engine.git](https://github.com/diegoagudoa-eng/portfolio-optimization-risk-engine.git)
   cd portfolio-optimization-risk-engine
