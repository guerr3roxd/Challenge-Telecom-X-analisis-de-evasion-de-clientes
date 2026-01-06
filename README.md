# Challenge Telecom X – Análisis de evasión de clientes

Este proyecto realiza un análisis exploratorio y de limpieza de datos sobre clientes de una empresa de telecomunicaciones ficticia, con foco en entender los factores asociados a la evasión de clientes (*churn*).

El objetivo principal es preparar un conjunto de datos limpio y estructurado que permita construir modelos de Machine Learning para predecir qué clientes tienen mayor probabilidad de abandonar el servicio.

---

## 📊 Datos del proyecto

- **Repositorio de este análisis:**  
  https://github.com/guerr3roxd/Challenge-Telecom-X-analisis-de-evasion-de-clientes

- **Fuente original de datos (JSON):**  
  https://raw.githubusercontent.com/ingridcristh/challenge2-data-science-LATAM/refs/heads/main/TelecomX_Data.json

El archivo JSON contiene información anidada en secciones como `customer`, `phone`, `internet` y `account`, que se normalizan y combinan en un único DataFrame para su análisis.

---

## 🏗️ Estructura general del análisis

El trabajo se organiza en un notebook (o Google Colab) con las siguientes etapas principales:

### 1️⃣ Extracción y normalización

- Carga del JSON desde GitHub usando `pandas.read_json`.
- Normalización de las estructuras anidadas (`customer`, `phone`, `internet`, `account`) con `pd.json_normalize`.
- Unión de todas las tablas en un único DataFrame de trabajo.

### 2️⃣ Limpieza y transformación

- Conversión de columnas numéricas como `Charges.Monthly` y `Charges.Total` a tipo flotante, manejando valores no válidos con `errors="coerce"`.
- Conversión de múltiples columnas con valores `Yes/No`, `1/0`, `No phone service` y `No internet service` a tipo booleano mediante funciones auxiliares.
- Eliminación de filas sin información en la columna `Churn`, ya que impiden analizar correctamente la evasión.
- Conversión de identificadores y categorías (`customerID`, `gender`, `InternetService`, `Contract`, `PaymentMethod`) a tipo texto/categórico.
- Creación de columnas derivadas como `Charges.Daily` para representar el gasto diario del cliente a partir de `Charges.Monthly`.

### 3️⃣ Análisis exploratorio (EDA)

- Estadísticos descriptivos de columnas numéricas como `tenure`, `Charges.Monthly`, `Charges.Total` y `Charges.Daily`.
- Resumen de columnas categóricas y booleanas: distribución de `Churn`, género, tipo de contrato, método de pago y servicios contratados.
- Discusión de la importancia de `Churn` como variable objetivo para entender el abandono de clientes.

### 4️⃣ Resultado final

DataFrame final con:
- Columnas numéricas y booleanas correctamente tipadas.
- Filas con `Churn` vacío eliminadas, quedando 7.043 registros válidos.
- Variables derivadas útiles para posteriores modelos de clasificación y segmentación.

---

## 💻 Requisitos y ejecución

### Requisitos

Se recomienda usar **Python 3.8+** con las siguientes librerías:

```
pandas
numpy
matplotlib
seaborn
```

### Ejecución local

1. Clonar este repositorio:
   ```bash
   git clone https://github.com/guerr3roxd/Challenge-Telecom-X-an-lisis-de-evasi-n-de-clientes.git
   cd Challenge-Telecom-X-an-lisis-de-evasi-n-de-clientes
   ```

2. Crear y activar un entorno virtual (opcional pero recomendado):
   ```bash
   python -m venv venv
   source venv/bin/activate  # En Windows: venv\Scripts\activate
   ```

3. Instalar dependencias:
   ```bash
   pip install -r requirements.txt
   ```

4. Abrir el notebook en Jupyter:
   ```bash
   jupyter notebook
   ```

5. Ejecutar las celdas en orden, comenzando por la sección de **Extracción** para garantizar que todos los datos se carguen y transformen correctamente.

### Ejecución en Google Colab

1. Abrir un nuevo notebook en Google Colab.
2. Copiar las celdas del notebook del repositorio.
3. Ejecutar las celdas de forma secuencial, partiendo por la importación y normalización de datos.

---

## 📝 Notas sobre el dataset

- La columna **`Churn`** es la variable objetivo, usada para identificar si un cliente abandona o no la empresa.
- Existen varias columnas binarias que se transforman a booleanas para facilitar el análisis (`Partner`, `Dependents`, `PhoneService`, servicios de Internet y de soporte, entre otras).
- Algunas filas con `Churn` vacío se eliminan, ya que no aportan información para el análisis de evasión.
- Se crea la columna `Charges.Daily` a partir de `Charges.Monthly / 30.44` para estimar un costo diario más realista.

---

## 📊 Dataset final

| Columna | Tipo | Descripción |
|---------|------|-------------|
| `customerID` | string | Identificador único del cliente |
| `Churn` | bool | Si el cliente abandonó la empresa |
| `gender` | string | Género del cliente |
| `SeniorCitizen` | bool | Si es ciudadano senior (≥65 años) |
| `Partner` | bool | Si el cliente tiene pareja |
| `Dependents` | bool | Si el cliente tiene dependientes |
| `tenure` | int | Meses de contrato |
| `PhoneService` | bool | Suscripción al servicio telefónico |
| `InternetService` | string | Tipo de servicio de internet |
| `Contract` | string | Tipo de contrato |
| `PaymentMethod` | string | Método de pago |
| `Charges.Monthly` | float | Cargos mensuales en USD |
| `Charges.Total` | float | Cargos totales acumulados en USD |
| `Charges.Daily` | float | Cargos diarios aproximados en USD |

**Dimensiones finales:** 7.043 filas × 22 columnas

---

## 🎯 Origen del desafío

Este proyecto se desarrolla a partir del desafío de ciencia de datos de **Alura Latam – Telecom X**, cuyo objetivo es apoyar a la empresa en la comprensión de su alta tasa de cancelación de clientes mediante el análisis de datos estructurados.

---

## 📄 Licencia

Este proyecto se distribuye bajo licencia MIT. Consulta el archivo `LICENSE` para más detalles.

---

**Última actualización:** 05 de Enero, 2026  
**Versión:** 2.1 - Código optimizado y corregido
