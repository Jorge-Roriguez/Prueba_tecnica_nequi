# Prueba_tecnica_nequi

# 🚦 Detección de Fraccionamiento Transaccional – Nequi

## 📌 Propósito del proyecto

Este proyecto tiene como objetivo detectar **fraccionamiento transaccional**, una mala práctica que consiste en dividir una transacción grande en múltiples operaciones pequeñas dentro de una ventana corta de tiempo (24 horas), realizadas por el mismo usuario o desde la misma cuenta.

Detectar este patrón permite mitigar riesgos financieros y fortalecer los controles operativos en canales digitales.

---

## 🧠 Enfoque de la solución

Se desarrolló un modelo **heurístico explicativo** en Python, capaz de identificar comportamientos sospechosos de fraccionamiento con base en reglas claras y replicables.

### 👣 Flujo de trabajo
1. **Carga de datos** en formato `.parquet`
2. **Conversión de fechas** y extracción del componente diario
3. **Agrupación** por `user_id` y `fecha`
4. **Cálculo de métricas**: número de transacciones, monto total, promedio y desviación estándar
5. **Regla de negocio aplicada**:
   - ≥ 5 transacciones en el mismo día
   - suma de montos ≥ percentil 95 global
6. **Identificación de casos sospechosos**
7. **Exportación** de resultados para visualización o análisis posterior

---

## 🔍 Exploración de los datos (EDA)

- Se validó calidad de los datos: tipos, nulos y duplicados.
- Se identificaron patrones en los montos y frecuencia por usuario.
- Se observó que el fraccionamiento puede estar concentrado en pocos usuarios con alta actividad diaria.

> Herramientas utilizadas: `pandas`, `matplotlib`, `seaborn`

---

## ⚙️ Modelo heurístico propuesto

```python
# Criterios para marcar sospechoso
if num_txns >= 5 and suma_montos >= percentil_95:
    marcar como sospechoso
