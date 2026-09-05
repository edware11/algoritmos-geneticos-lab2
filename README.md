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

## Ejercicio 4 — Análisis de Resultados
