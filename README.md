# Simulación con Modelo Oculto de Markov (HMM)
## Predicción Climática basada en Observaciones de Humedad

**Asignatura:** Simulación — Módulo 2, Actividad Didáctica 2
**Tema:** Distribuciones de probabilidad y Cadenas de Markov

---

## Descripción

Este proyecto implementa un **Modelo Oculto de Markov (HMM)** para simular y predecir condiciones climáticas (Soleado, Nublado, Lluvioso) a partir de observaciones de humedad ambiental (Baja, Media, Alta). El modelo demuestra cómo representar procesos estocásticos con información no directamente observable.

---

## Archivos del Proyecto

| Archivo | Descripción |
|---|---|
| `hmm_clima.py` | Código principal con la implementación del HMM, simulación de 30 días, visualizaciones y estadísticas |
| `README.md` | Este archivo: instrucciones y documentación del proyecto |
| `simulacion_hmm.png` | Gráfico generado: secuencia temporal de estados y observaciones (se crea al ejecutar) |
| `estadisticas_hmm.png` | Gráfico generado: distribuciones y matriz de confusión (se crea al ejecutar) |

---

## Requisitos

### Librerías Python necesarias

```
numpy
matplotlib
```

---

## Instrucciones de Ejecución

### Opción 1: Google Colab

1. Abrir [Google Colab](https://colab.research.google.com) en el navegador.
2. Crear un nuevo notebook (`Archivo → Nuevo cuaderno`).
3. En la primera celda, instalar dependencias (si es necesario):
4. Copiar y pegar el contenido completo de `hmm_clima.py` en una nueva celda.
5. Ejecutar la celda con `Shift + Enter` o el botón de play.
6. Los gráficos se mostrarán directamente en el notebook.

### Opción 2: Jupyter Notebook (local)

1. Asegurarse de tener Jupyter instalado:
   ```bash
   pip install jupyter
   ```
2. Abrir Jupyter en el directorio del proyecto:
   ```bash
   jupyter notebook
   ```
3. Crear un nuevo notebook Python 3.
4. Copiar el contenido de `hmm_clima.py` en una celda y ejecutar.

### Opción 3: Terminal / Línea de comandos

```bash
# Ejecutar la simulación principal
python hmm_clima.py

```

---

## Parámetros del Modelo

### Estados ocultos (clima)
- **Soleado** (color: amarillo `#FFD700`)
- **Nublado** (color: azul claro `#87CEEB`)
- **Lluvioso** (color: azul oscuro `#1E3A5F`)

### Observaciones (humedad)
- Humedad Baja
- Humedad Media
- Humedad Alta

### Distribución inicial (π)
| Estado | Probabilidad |
|---|---|
| Soleado | 0.6 |
| Nublado | 0.3 |
| Lluvioso | 0.1 |

### Matriz de Transición (A)
|  | Soleado | Nublado | Lluvioso |
|---|---|---|---|
| **Soleado** | 0.7 | 0.2 | 0.1 |
| **Nublado** | 0.3 | 0.4 | 0.3 |
| **Lluvioso** | 0.2 | 0.3 | 0.5 |

### Matriz de Emisión (B)
|  | Hum. Baja | Hum. Media | Hum. Alta |
|---|---|---|---|
| **Soleado** | 0.7 | 0.2 | 0.1 |
| **Nublado** | 0.2 | 0.5 | 0.3 |
| **Lluvioso** | 0.1 | 0.3 | 0.6 |

---

## Salida esperada en consola

```
====================================================
  PRIMERAS 10 OBSERVACIONES DE LA SIMULACIÓN
====================================================
  Día  1: Soleado     →  Humedad Baja
  Día  2: Soleado     →  Humedad Baja
  Día  3: Soleado     →  Humedad Baja
  ...
====================================================

====================================================
  ESTADÍSTICAS DE LA SIMULACIÓN (30 días)
====================================================

  Días en cada estado climático:
    Soleado   : XX días (XX.X%)  ████...
    Nublado   : XX días (XX.X%)  ████...
    Lluvioso  : XX días (XX.X%)  ████...

  Porcentaje de humedad observada:
    Humedad Baja   :  XX.X%
    Humedad Media  :  XX.X%
    Humedad Alta   :  XX.X%

  Matriz de confusión (Estado × Observación):
              Baja     Media      Alta
    Soleado      X         X         X
    Nublado      X         X         X
    Lluvioso     X         X         X
====================================================
```

---

## Evidencias de Resultados

### Gráfico 1 — Secuencia temporal (`simulacion_hmm.png`)

El gráfico muestra dos paneles alineados verticalmente para los 30 días simulados:

- **Panel superior:** Barras coloreadas representando el **estado climático oculto** de cada día.
  - Amarillo = Soleado
  - Azul claro = Nublado
  - Azul oscuro = Lluvioso

- **Panel inferior:** Barras coloreadas representando el **nivel de humedad observado** de cada día, alineado con el panel superior.

```
Ejemplo de estructura visual (días 1-10):
Día:    1    2    3    4    5    6    7    8    9   10
        [Sol][Sol][Sol][Nub][Sol][Sol][Nub][Nub][Sol][Llo]  ← Estados
        [Baj][Baj][Med][Med][Baj][Baj][Med][Alt][Baj][Alt]  ← Humedad
```

### Gráfico 2 — Estadísticas (`estadisticas_hmm.png`)

Tres subgráficos con información estadística agregada:

1. **Gráfico circular (torta):** Proporción de días en cada estado climático.
2. **Gráfico de barras:** Porcentaje de cada nivel de humedad observado en los 30 días.
3. **Mapa de calor:** Matriz de confusión que muestra la relación entre estados ocultos y observaciones emitidas.

### Resultado esperado con semilla `np.random.seed(42)`

Con la semilla fija de aleatoriedad, la simulación produce resultados reproducibles:

- Los días soleados predominan (coherente con π inicial = 0.6 y A[Sol→Sol] = 0.7).
- La humedad baja es más frecuente (coherente con B[Sol→Baja] = 0.7 y predominio solar).
- La diagonal de la matriz de confusión refleja la coherencia entre estados y sus emisiones más probables.

---

## Estructura de la Solución

```
├── Instrucciones.md          # Enunciado de la actividad
├── hmm_clima.py              # Código principal HMM
├── generar_documento.py      # Generador del documento Word
├── README.md                 # Este archivo
├── simulacion_hmm.png        # Gráfico generado (tras ejecutar)
├── estadisticas_hmm.png      # Gráfico generado (tras ejecutar)
```

---

## Conceptos Clave

| Concepto | Descripción |
|---|---|
| **Estado oculto** | Condición real del sistema que no se puede observar directamente (clima) |
| **Observación** | Señal medible relacionada con el estado oculto (humedad) |
| **π (inicial)** | Probabilidad de comenzar en cada estado |
| **A (transición)** | Probabilidad de pasar de un estado a otro entre pasos |
| **B (emisión)** | Probabilidad de observar cada símbolo dado el estado actual |
| **Proceso de Markov** | La transición solo depende del estado actual, no del historial |
