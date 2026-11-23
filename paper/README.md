# El paper — el benchmark detrás del método

**Can LLM Agents Be Used to Scale Evaluation Tasks? A Preregistered Test of Instance Interchangeability in Translation Quality Assessment**
Romina Pitronello (autoría única). Manuscrito de agosto de 2026. Desde noviembre de 2026 es un preprint sin revisión por pares, con otro título: *Instances of the Same LLM Were Not Interchangeable Raters Where the Task Required Judgment: A Registered, Author-Blind Test on a Translation-Quality Battery at Temperature 0 and 1*, Zenodo, doi [10.5281/zenodo.24447506](https://doi.org/10.5281/zenodo.24447506).

- Preregistro: https://osf.io/zusb5
- Datos, código y materiales: https://osf.io/ue4qy
- ORCID: 0009-0005-5159-6339
- Manuscrito (versión de agosto de 2026, 26 páginas; el preprint de Zenodo es la versión vigente): `Pitronello_2026_BRM_instance_interchangeability.pdf`
- Scripts del análisis, tal como corrieron: `analysis_prereg.py` (el análisis confirmatorio preregistrado) y `sensitivity_analyses.py`. Los datos completos están en OSF.

## La pregunta

Si usas un LLM como juez a escala — para evaluar traducciones, CVs, transacciones, lo que sea — ¿puedes tratar dos instancias del mismo modelo como intercambiables? La práctica de la industria asume que sí. Este estudio lo pone a prueba.

## El diseño

- Diseño factorial 3 × 4 × 2. 480 instancias de agentes (457 válidas).
- Batería propia de 11 ítems en 16 categorías de juicio (tipología Delta-pi).
- Preregistrado antes de recolectar datos. Análisis confirmatorio ejecutado por un agente Claude Fable 5 con la autora ciega a los datos, como parte del blinding.
- Instrumento co-producido con Claude Opus.

## El hallazgo

Las instancias de un mismo modelo **no son intercambiables** como jueces. La divergencia entre instancias se estructura por tipo de juicio — llega a 2,7× según la categoría — y **persiste a temperatura cero**. Temperatura cero garantiza decodificación greedy dentro de una instancia; no garantiza que dos instancias en distinto hardware, batch o momento produzcan lo mismo. En tareas de juicio, esa diferencia no es ruido marginal.

## Por qué está en este repo

Porque es lo que Romina usa cuando trabaja, no un adorno académico. Tres lugares donde el paper gobierna decisiones en `transcripts/`:

1. **Contra código, frozen** (`04`, 00:55): rechaza que un modelo haga análisis de varianza por aritmética propia, porque midió que fallan en cálculo sin código.
2. **Dos réplicas, acuerdo = válido** (`conector-mcp/`): ninguna categoría de juicio entra al esquema con una sola lectura de Haiku. El esquema de la casa asume varianza inter-instancia porque la midió.
3. **Las cinco preguntas de la sonda** (`02`, 12:50): el prompt del orquestador cierra con una frase sobre por qué un solo intercambio no revela la instancia — *es* la instancia. Viene directo del marco del paper.

Un CTO que quiera usar agentes como evaluadores en producción — de fraude, de riesgo, de soporte — necesita saber cuánto varía el juicio entre instancias antes de confiar en un solo run. Este paper mide exactamente eso, y la persona que lo escribió construye harnesses que lo asumen.
