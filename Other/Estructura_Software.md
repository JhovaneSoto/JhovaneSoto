# 📂 Estructura de Documentación del Proyecto de Software

| Archivo | Propósito principal |
|----------|----------------------|
| **01_vision_general.md** | Define el propósito, alcance y objetivos del proyecto. |
| **02_requerimientos.md** | Lista lo que el sistema debe hacer (funcional y técnico). |
| **03_diseno_arquitectura.md** | Explica cómo se organiza el código y los módulos. |
| **04_flujo_de_trabajo.md** | Describe el proceso interno (cómo fluye la información). |
| **05_plan_desarrollo.md** | Fases, entregables y prioridades del proyecto. |
| **06_estrategias_trading.md** | Define las reglas, estrategias o algoritmos que usará el bot. |
| **07_configuracion_api.md** | Explica cómo conectar y autenticar con Binance (Test y Real). |
| **08_pruebas_y_validacion.md** | Define cómo probarás que todo funciona correctamente. |
| **09_notas_y_mejoras.md** | Espacio para apuntes, ideas y mejoras futuras. |

---

## 📘 Contenido general de cada archivo

---

### 1️⃣ 01_vision_general.md

**Propósito:** describir el qué y el por qué del proyecto.

#### Contenido sugerido

# Visión General

## Propósito
Desarrollar un bot automatizado para realizar microtransacciones de trading en Binance, con enfoque en precisión, seguridad y aprendizaje automático a futuro.

## Objetivos
- Realizar compras y ventas automáticas de criptomonedas.
- Operar con montos pequeños (~$0.10 USD).
- Registrar y analizar resultados de las operaciones.
- Probar estrategias sin riesgo en la red de prueba (Testnet).

## Alcance
Incluye: conexión a API, ejecución de órdenes, registro de datos y análisis básico.  
No incluye (por ahora): estrategias con machine learning ni trading de alto volumen.

## Motivación
Proyecto personal para aprender automatización financiera y manejo de APIs reales.

---

### 2️⃣ 02_requerimientos.md

**Propósito:** dejar claro qué debe hacer el sistema y con qué se construirá.

#### Contenido sugerido

# Requerimientos

## Requerimientos funcionales
- Conectarse a la API de Binance (Testnet y Real).
- Obtener precios en tiempo real.
- Ejecutar órdenes de compra/venta.
- Registrar operaciones en archivo o base de datos local.
- Mostrar logs o resultados en consola o interfaz.

## Requerimientos no funcionales
- Código modular, limpio y documentado.
- Manejo seguro de claves API.
- Permitir configuración desde un archivo JSON.
- Soportar reconexión automática en caso de fallo.

## Tecnologías
- Python 3.11+
- Librerías: `python-binance`, `pandas`, `dotenv`, `requests`, `logging`, `PyQt5` (opcional)
- Entorno virtual con `venv`

---

### 3️⃣ 03_diseno_arquitectura.md

**Propósito:** visualizar cómo se conectan las partes del proyecto.

#### Contenido sugerido

# Diseño de Arquitectura

## Estructura general
CobraTrade/
│
├─ src/
│ ├─ main.py
│ ├─ modules/
│ │ ├─ binance_api.py
│ │ ├─ strategy.py
│ │ ├─ logger.py
│ │ └─ utils.py
│ └─ config/settings.json
│
└─ data/
├─ trades_log.csv
└─ errors.log


## Descripción de módulos
- **main.py:** punto de entrada del programa.
- **binance_api.py:** conexión y autenticación con la API.
- **strategy.py:** contiene la lógica de trading (cuándo comprar o vender).
- **logger.py:** gestiona los registros y logs del sistema.
- **utils.py:** funciones auxiliares (manejo de tiempos, conversiones, etc.).

## Diagrama de flujo
(API ↔ Bot ↔ Logs/DB ↔ Interfaz)

---

### 4️⃣ 04_flujo_de_trabajo.md

**Propósito:** documentar el proceso lógico que seguirá el programa.

#### Contenido sugerido

# Flujo de Trabajo

1. Iniciar conexión a la API (clave y secreto desde `.env`).
2. Consultar precios actuales de los pares definidos.
3. Evaluar estrategia (ej. si el precio bajó 1%, comprar).
4. Ejecutar orden y confirmar respuesta.
5. Registrar resultado (hora, monto, resultado, balance).
6. Esperar un tiempo definido antes de la siguiente operación.

---

### 5️⃣ 05_plan_desarrollo.md

**Propósito:** definir fases, prioridades y entregables.

#### Contenido sugerido

# Plan de Desarrollo

## Fases del Proyecto

| Fase | Descripción | Estado |
|------|--------------|--------|
| 1 | Configurar entorno y API de Binance Testnet | 🔄 En progreso |
| 2 | Ejecutar órdenes simples (manuales) | ⏳ Pendiente |
| 3 | Implementar estrategia automática | ⏳ Pendiente |
| 4 | Agregar logs y registro de operaciones | ⏳ Pendiente |
| 5 | Añadir interfaz (opcional) | ⏳ Pendiente |

## Entregables
- Código funcional para testnet.
- Archivo de configuración.
- Logs con historial de operaciones.

---

### 6️⃣ 06_estrategias_trading.md

**Propósito:** detallar la lógica detrás de las decisiones del bot.

#### Contenido sugerido

# Estrategias de Trading

## Estrategia base
- Compra cuando el precio baja un X% respecto al promedio de los últimos N minutos.
- Vende cuando sube un Y%.

## Ejemplo
- Umbral de compra: -0.5%
- Umbral de venta: +0.8%
- Intervalo de chequeo: cada 10 segundos

## Posibles mejoras futuras
- Incorporar RSI, MACD o medias móviles.
- Estrategias basadas en volumen o tendencia.
- Integración con IA para predicción.

---

### 7️⃣ 07_configuracion_api.md

**Propósito:** documentar cómo usar las claves y endpoints correctamente.

#### Contenido sugerido

# Configuración de la API de Binance

## Testnet
- URL: https://testnet.binance.vision
- Crear claves API desde la web de Binance Testnet.
- Guardar en archivo `.env`:

API_KEY=tu_api_key
API_SECRET=tu_api_secret


## Real
- Cambiar las URLs al entorno real cuando esté probado.

---

### 8️⃣ 08_pruebas_y_validacion.md

**Propósito:** asegurar calidad antes de pasar a producción.

#### Contenido sugerido

# Pruebas y Validación

## Pruebas unitarias
- Testear conexión con API.
- Testear ejecución de orden (simulada).
- Testear funciones de estrategia.

## Pruebas funcionales
- Simular una sesión de trading de 1 hora.
- Revisar que los logs se guarden correctamente.
- Validar reconexión automática ante fallos de red.

---

### 9️⃣ 09_notas_y_mejoras.md

**Propósito:** mantener registro de ideas, errores o cosas por agregar.

#### Contenido sugerido

# Notas y Mejoras

## Observaciones
- A veces la API responde con retraso → manejar reintentos.
- Evaluar agregar manejo de excepciones personalizadas.

## Ideas futuras
- Dashboard visual con PyQt5.
- Exportar datos a Google Sheets.
- Alertas vía Telegram o correo.
