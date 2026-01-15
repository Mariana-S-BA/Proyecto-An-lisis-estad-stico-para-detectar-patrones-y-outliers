# Proyecto 6 — Análisis de una empresa de telecomunicaciones (ConnectaTel)

## Objetivo del proyecto
Este proyecto analiza el comportamiento real de uso móvil (llamadas y mensajes) de clientes de **ConnectaTel** (México y Colombia), con el fin de:
- Identificar **patrones de uso** por tipo de cliente.
- Detectar **comportamientos atípicos (outliers)** que puedan indicar fraude, errores de captura o necesidades especiales.
- Construir **segmentaciones** accionables por edad y nivel de uso.
- Proponer **recomendaciones comerciales** para optimizar la oferta de planes y mejorar la experiencia del usuario.

---

## Datasets utilizados
El análisis se construye integrando 3 fuentes de datos en formato CSV:

- **`plans.csv`**: catálogo de planes (precio, minutos/GB incluidos, costo por extra).
- **`users_latam.csv`**: información del cliente (edad, ciudad, fecha de registro, plan contratado, churn).
- **`usage.csv`**: registro de uso (tipo de evento: llamadas o mensajes, duración/longitud, fecha).

> Los datasets se complementan para analizar consumo, segmentación y variaciones por plan y edad.

---

## Estructura del repositorio
- `notebook.ipynb` (o el nombre de tu notebook): análisis completo, limpieza, visualizaciones, segmentación e insights.
- `datasets/` (opcional si incluyes datos localmente):
  - `plans.csv`
  - `users_latam.csv`
  - `usage.csv`
- `README.md`: descripción del proyecto y guía de ejecución.

---

## Etapas del análisis realizadas
1. **Carga y exploración**
   - Revisión de estructura (`.shape`, `.info()`, `.head()`).
2. **Calidad de datos**
   - Conteo y proporción de nulos (`isna().sum()`, `isna().mean()`).
   - Detección de sentinels y valores inválidos (`-999`, `"?"`, fechas fuera de rango).
3. **Limpieza básica**
   - Reemplazo de sentinels:
     - `age = -999` → `NaN` → imputación con mediana.
     - `city = "?"` → `NA`.
   - Estandarización de fechas y marcado de fechas futuras como `NaT`.
   - Validación de nulos en `usage` según `type` (llamada vs texto).
4. **Construcción de métricas por usuario**
   - Agregación de `usage` por `user_id`:
     - `cant_mensajes`, `cant_llamadas`, `cant_minutos_llamada`.
   - Unión con `users` para crear un perfil por usuario.
5. **Visualización y outliers**
   - Histogramas por plan (`hue="plan"`) para variables clave.
   - Boxplots para identificar outliers.
   - Revisión con método IQR (cuando aplica) para decidir si se mantienen o no.
6. **Segmentación**
   - Segmentación por **nivel de uso**: Bajo / Medio / Alto.
   - Segmentación por **edad**: Joven / Adulto / Adulto Mayor.
   - Visualización de segmentos con countplots.
7. **Insight ejecutivo**
   - Resumen de problemas de datos, segmentos encontrados, outliers y recomendaciones comerciales.

---

## Cómo ejecutar el notebook (Google Colab)
1. Abre Google Colab.
2. Sube el notebook (`.ipynb`) al entorno de Colab.
3. Asegúrate de tener los datasets disponibles:
   - Opción A: subir los CSV manualmente a Colab (panel izquierdo → Files → Upload).
   - Opción B: montar Google Drive y leer desde ahí.
4. Instala dependencias si fuera necesario (normalmente ya vienen):
   ```bash
   pip install pandas numpy matplotlib seaborn
