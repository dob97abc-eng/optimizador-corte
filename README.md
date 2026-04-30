# ✦ Optimizador de Corte 1D

Herramienta web para planificación de cortes de material lineal (vigas, tubos, perfiles, madera, etc.) que **minimiza el desperdicio** usando programación lineal entera con solver ILP industrial.

---

## ¿Qué hace?

Dado un largo de barra estándar y una lista de piezas a cortar, la herramienta calcula el **plan de corte óptimo**: cuántas barras usar, cómo distribuir los cortes en cada una, y cuánto material se desperdicia — garantizando que no existe una solución mejor.

---

## Demo

🔗 **[Abrir herramienta]https://MPLSOLUTIONS.github.io/optimizador-corte/**

---

## Características

- **Solución óptima garantizada** — usa `scipy.optimize.milp` con solver HiGHS, el mismo estándar industrial
- **Sin instalación** — corre 100% en el navegador (Pyodide + WebAssembly)
- **Patrones agrupados** — muestra cuántas barras comparten el mismo patrón de corte, no una lista interminable
- **Visualización clara** — cada barra muestra sus cortes a escala con colores por tipo de pieza
- **Fallback automático** — si el solver Python no está disponible, usa un algoritmo FFD + Branch & Bound en JavaScript
- **Kerf configurable** — incluye el ancho de corte de la sierra en los cálculos
- **Ejemplo precargado** — viene con un caso de prueba listo para usar

---

## Cómo usar

1. Ingresa el **largo de tu barra estándar** (ej: 3200 mm, 6000 mm)
2. Ingresa el **ancho de corte** de tu sierra (kerf, ej: 3 mm)
3. Agrega las **piezas que necesitas** con su largo y cantidad
4. Presiona **Optimizar cortes**
5. Espera que el solver calcule (puede tomar 10-30 segundos la primera vez mientras carga)
6. Revisa el **plan de corte** con patrones agrupados y estadísticas de eficiencia

---

## Tecnología

| Componente | Detalle |
|---|---|
| **Solver** | `scipy.optimize.milp` con HiGHS (ILP industrial) |
| **Runtime Python** | Pyodide 0.25 (Python 3.11 en WebAssembly) |
| **Algoritmo** | Enumeración completa de patrones + MILP |
| **Fallback** | First Fit Decreasing + Branch & Bound en JS |
| **Frontend** | HTML + CSS + JavaScript puro, sin frameworks |

---

## Contexto técnico

El problema de corte 1D es conocido como **Cutting Stock Problem (CSP)**, clasificado como NP-hard. La herramienta lo resuelve en dos pasos:

1. **Generación de patrones**: enumera todas las combinaciones de piezas que caben en una barra (hasta 50.000 patrones)
2. **MILP**: formula el problema como minimizar el número de barras sujeto a cubrir la demanda de cada tipo de pieza, y lo resuelve con HiGHS

Para instancias típicas de uso en construcción o manufactura (hasta ~15 tipos de piezas, ~200 unidades), encuentra el óptimo global en segundos.

---

## Limitaciones

- La primera carga tarda ~15-30 segundos (descarga Pyodide ~30MB, solo una vez)
- Para instancias muy grandes (+20 tipos de piezas con alta demanda), el tiempo de resolución puede aumentar
- Requiere conexión a internet para cargar Pyodide desde CDN

---

## Desarrollo

Desarrollado por **Matías Parra** para planificación de cortes en proyectos forestales e industriales.

---

## Licencia

MIT — libre para uso personal y comercial.
