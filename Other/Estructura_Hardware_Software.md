# 📂 Estructura de Documentación del Proyecto de Hardware y Software

| Archivo | Propósito principal |
|----------|----------------------|
| **01_vision_general.md** | Explica qué hace el proyecto, para qué sirve y cuál es su objetivo. |
| **02_requerimientos.md** | Define qué componentes electrónicos, materiales y software se necesitan. |
| **03_diseno_circuito.md** | Describe el circuito electrónico, conexiones, esquemas y componentes. |
| **04_firmware_y_software.md** | Explica el código del microcontrolador y la comunicación con el software. |
| **05_flujo_de_operacion.md** | Muestra el flujo lógico (cómo interactúan hardware y software). |
| **06_plan_desarrollo.md** | Plan de fases, pruebas, tiempos y entregables. |
| **07_pruebas_y_validacion.md** | Cómo se prueban los circuitos, firmware y comunicación. |
| **08_resultados_y_ajustes.md** | Registra observaciones, resultados y mejoras. |
| **09_notas_y_versiones.md** | Control de versiones, notas técnicas e ideas futuras. |

---

## 📘 Contenido general de cada archivo

---

### 1️⃣ 01_vision_general.md

**Propósito:** tener claro qué hace el proyecto y qué problema resuelve.

#### Ejemplo de contenido

# Visión General

## Nombre del proyecto
Pomodoro Hardware Timer

## Descripción
Temporizador físico basado en un **Arduino Nano** con un **LED RGB** y un **buzzer** para indicar las fases de trabajo y descanso del método Pomodoro.

## Objetivos
- Implementar un ciclo automático de trabajo/descanso usando un microcontrolador.
- Mostrar el estado mediante un LED RGB.
- Emitir sonidos cuando cambia de fase.
- Permitir modificar los tiempos desde software o botones físicos.

## Alcance
Incluye: diseño del circuito, programación del firmware y pruebas.  
No incluye: interfaz gráfica en PC ni conexión inalámbrica (por ahora).

---

### 2️⃣ 02_requerimientos.md

**Propósito:** definir lo que necesitas a nivel técnico y material.

# Requerimientos

## Materiales y componentes
| Componente | Descripción | Cantidad |
|-------------|--------------|-----------|
| Arduino Nano | Microcontrolador principal | 1 |
| LED RGB | Indicador visual del estado | 1 |
| Buzzer | Alarma sonora | 1 |
| Resistencias de 220Ω | Limitadoras de corriente LED | 3 |
| Pulsador | Para iniciar/pausar ciclo | 1 |
| Protoboard y cables | Conexión temporal | Varios |

## Herramientas de software
- Arduino IDE o PlatformIO  
- Librerías: `Adafruit_NeoPixel` (si usas LED direccionable)  
- (Opcional) Python + PySerial para control externo

## Requerimientos funcionales
- Indicar con colores las fases (rojo = trabajo, verde = descanso).  
- Activar buzzer al cambiar de fase.  
- Controlar tiempos de ciclo predefinidos (25/5 min).  
- Mostrar estado en serie (para depuración).

---

### 3️⃣ 03_diseno_circuito.md

**Propósito:** detallar cómo se conecta todo y cómo se comporta eléctricamente.

# Diseño del Circuito

## Esquema general
El circuito conecta:
- LED RGB a los pines D9, D10, D11.  
- Buzzer al pin D3.  
- Pulsador al pin D2 con resistencia pull-down.

## Diagrama (texto o imagen)
[D2] ← Pulsador
[D3] → Buzzer
[D9-D11] → LED RGB
[GND] → Común
[+5V] → Alimentación

yaml
Copiar código

*(Aquí puedes incluir un esquema desde Fritzing o KiCad)*

## Consideraciones
- Las resistencias protegen los LEDs.  
- El buzzer debe ser de tipo activo (no pasivo) si no se genera PWM.  
- Fuente de alimentación por USB o 5V externa.

---

### 4️⃣ 04_firmware_y_software.md

**Propósito:** explicar la lógica del código y su relación con el hardware.

# Firmware y Software

## Firmware (Arduino)
El firmware controla los ciclos Pomodoro:
1. Inicia en estado "trabajo" (LED rojo).  
2. Al completar el tiempo, pasa a "descanso" (LED verde).  
3. Suena el buzzer entre fases.  
4. Permite reinicio manual con pulsador.

## Pseudocódigo
loop:
si estado == trabajo y tiempo cumplido:
cambiar a descanso
sonar buzzer
si estado == descanso y tiempo cumplido:
cambiar a trabajo
sonar buzzer

yaml
Copiar código

## Comunicación externa (opcional)
Si se conecta a un PC:
- Enviar estado actual por puerto serie (ej: `STATE:WORK`).  
- Recibir comandos desde Python (ej: `SET 20 5` para cambiar tiempos).

---

### 5️⃣ 05_flujo_de_operacion.md

**Propósito:** mostrar gráficamente cómo fluye la información y las acciones.

# Flujo de Operación

1️⃣ Usuario presiona botón "Inicio".  
2️⃣ Arduino inicia temporizador → LED rojo.  
3️⃣ Al terminar el ciclo → buzzer + LED verde.  
4️⃣ Espera periodo de descanso.  
5️⃣ Repite ciclo o pausa manualmente.

## Diagrama
Usuario → Pulsador → Arduino → LED/Buzzer → Feedback

yaml
Copiar código

---

### 6️⃣ 06_plan_desarrollo.md

**Propósito:** dividir el proyecto en fases lógicas.

# Plan de Desarrollo

| Fase | Tarea | Estado |
|------|--------|--------|
| 1 | Prototipo en protoboard | ✅ Listo |
| 2 | Programar firmware base | 🔄 En progreso |
| 3 | Probar temporizador y buzzer | ⏳ Pendiente |
| 4 | Integrar pulsador de control | ⏳ Pendiente |
| 5 | Optimizar código y depurar | ⏳ Pendiente |
| 6 | Documentar resultados | ⏳ Pendiente |

---

### 7️⃣ 07_pruebas_y_validacion.md

**Propósito:** definir cómo comprobar que el circuito y firmware funcionan.

# Pruebas y Validación

## Pruebas de hardware
- Verificar que cada LED cambia correctamente según el pin.  
- Confirmar buzzer activo en cambios de fase.  
- Pulsador responde en menos de 200ms.

## Pruebas de software
- Temporizador cambia tras 25 minutos.  
- Reset manual reinicia ciclo.  
- Comunicación serie muestra estados esperados.

## Registro de pruebas
| Fecha | Prueba | Resultado | Observaciones |
|--------|--------|------------|----------------|
| 10/11/2025 | LED rojo encendido | ✅ | Funciona |
| 10/11/2025 | Buzzer no suena | ❌ | Revisar pin D3 |

---

### 8️⃣ 08_resultados_y_ajustes.md

**Propósito:** anotar mediciones, fallas y mejoras detectadas.

# Resultados y Ajustes

## Observaciones
- El buzzer activo funcionó mejor con PWM.  
- LED verde algo débil → reemplazar resistencia por 150Ω.  
- Añadir retraso de seguridad antes de cambio de estado.

## Ajustes realizados
- Modificación de pines en firmware.  
- Reducción de tiempo de prueba a 10s/5s.

## Futuras mejoras
- Mostrar tiempo restante en pantalla OLED.  
- Agregar comunicación Bluetooth para configurar tiempos desde PC.

---

### 9️⃣ 09_notas_y_versiones.md

**Propósito:** mantener control técnico de versiones y aprendizajes.

# Notas y Versiones

## Versión 1.0
- Circuito básico en protoboard.  
- Firmware inicial con LED y buzzer.

## Versión 1.1
- Añadido pulsador de pausa.  
- Implementado control de tiempos desde serie.

## Notas adicionales
- Evaluar cambio a ESP32 para versión inalámbrica.  
- Documentar librerías usadas y su versión exacta.
