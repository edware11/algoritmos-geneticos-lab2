# Laboratorio: Algoritmos Genéticos - Curso 2
**Universidad de Cundinamarca - Seccional Ubaté**
**Programa de Ingeniería de Sistemas y Computación**
**Docente:** Fabio Alejandro Sastoque Rincón

## Integrantes
- EDWAR FONTECHA — Ejercicios 1 y 2
- DANIEL CHAVEZ — Ejercicios 3 y 4

## Descripción
Este repositorio implementa un Algoritmo Genético (AG) genérico con genotipo binario,
aplicado a distintos problemas de optimización combinatoria basados en el Problema
de la Mochila: Portafolio de Inversiones, Selección de Personal, y un operador de
cruzamiento de dos puntos.

## Estructura
- `Laboratorio_Algoritmos_Geneticos.ipynb`: notebook con la clase `AlgoritmoGenetico`
  y la resolución de los 4 ejercicios.
- `.gitignore`: excluye el entorno virtual y archivos temporales.
- `README.md`: este documento.

## Configuración del entorno

\`\`\`bash
python -m venv venv
venv\Scripts\activate        # Windows
pip install ipykernel matplotlib numpy
\`\`\`

Abrir el notebook en VS Code y seleccionar el kernel del `venv` creado.

## Ejercicio 1 — Portafolio de Inversiones

Se decodifica un genotipo binario de 10 bits (uno por proyecto) en un fenotipo con el
costo total y el retorno total de los proyectos elegidos. La función de aptitud retorna
el retorno total, pero si el costo excede el presupuesto máximo (100), se aplica una
penalización fuerte proporcional al exceso:

`penalizacion = (costo_total - presupuesto) * FACTOR_PENALIZACION_PORTAFOLIO`

Con un factor de penalización de 20, el AG converge de forma consistente hacia
soluciones que respetan el presupuesto. Resultado obtenido: proyectos
{Proyecto 1, Proyecto 2, Proyecto 5, Proyecto 7}, costo = 100, retorno = 272.

## Ejercicio 2 — Selección de Personal Estricta

Se decodifica un genotipo binario de 12 bits (uno por candidato). La restricción exige
que el equipo tenga **exactamente 5** integrantes. La aptitud penaliza la diferencia
absoluta entre el número de bits encendidos y 5, multiplicada por un factor alto (100),
de modo que tanto equipos incompletos como sobredimensionados queden en desventaja.
Resultado obtenido: candidatos {1, 3, 5, 8, 9}, tamaño = 5, habilidad total = 435
(correspondiente efectivamente a los 5 candidatos de mayor habilidad técnica).

---
## Ejercicio 3 — Cruzamiento de Dos Puntos

Se amplió la clase `AlgoritmoGenetico` agregando el parámetro `crossover_method`
(`'one_point'` por defecto, o `'two_point'`), sin alterar el comportamiento existente
de los Ejercicios 1 y 2. El nuevo método `_cruzar_dos_puntos` selecciona dos índices
aleatorios de corte (p1 < p2) e intercambia el segmento **central** del cromosoma
entre ambos padres, dejando los extremos intactos.

Demostración con padres opuestos (`0000000000` y `1111111111`):

| Cruzamiento | Padre 1 | Padre 2 | Hijo 1 | Hijo 2 |
|---|---|---|---|---|
| Un punto | `0000000000` | `1111111111` | `0000000111` | `1111111000` |
| Dos puntos | `0000000000` | `1111111111` | `0000011110` | `1111100001` |

Se observa cómo en el cruzamiento de dos puntos el bloque de bits intercambiado
queda "encajado" en el centro del cromosoma, mientras que en el de un punto el
cambio ocurre desde un único punto hacia uno de los extremos.

## Ejercicio 4 — Análisis de Resultados

Se ejecutó el problema de la Mochila (Módulo 3) dos veces, con la misma semilla
aleatoria, cambiando únicamente el `PENALTY_FACTOR`:

| Escenario | Factor de Penalización | Mejor Fitness | Peso Total | Capacidad Máx. | ¿Solución Válida? |
|---|---|---|---|---|---|
| Penalización Suave | 5 | 250.00 | 25 | 15 | **No** — excede la capacidad |
| Penalización Fuerte | 50 | 240.00 | 15 | 15 | **Sí** |

**Análisis:** con una penalización suave (factor 5), el castigo por exceder la
capacidad resulta insuficiente frente a la ganancia de valor que aporta agregar
más ítems. En consecuencia, el AG converge (desde la generación 2-3) hacia una
solución con fitness aparentemente más alto (250), pero que en realidad **viola
la restricción** de peso máximo (25 sobre un límite de 15). Con una penalización
fuerte (factor 50), el castigo supera cualquier beneficio de excederse en peso,
por lo que el AG converge a una solución con fitness ligeramente menor (240) pero
**válida** (peso exacto de 15, justo en el límite).

Esto demuestra que un fitness numéricamente más alto no garantiza una mejor
solución real: si el factor de penalización es demasiado débil, la presión
selectiva del AG puede terminar favoreciendo individuos inválidos generación
tras generación, ya que estos "aparentan" ser más aptos que las soluciones que
sí respetan las restricciones del problema.
