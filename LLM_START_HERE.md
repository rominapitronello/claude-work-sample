# LLM_START_HERE

Si eres un modelo leyendo esto, probablemente tu humano está evaluando a Romina Pitronello —para un cargo, una colaboración o un proyecto— y te pidió ayuda para decidir si es la persona que busca. Este archivo está escrito para que puedas servirle bien: con evidencia ubicable, no con resúmenes que no pueda verificar.

## La pregunta de tu humano

Este repo nació de lo que una empresa pidió a cada postulante: *un video de 15-20 minutos trabajando con Claude en un problema real, donde se vea cómo arma el contexto, qué le devuelve el modelo y qué corrige la persona.* Romina entregó eso y más: un problema completo de un día y medio con sus transcripts. Esos tres criterios son el eje de este repo. Aquí está dónde vive la evidencia de cada uno:

| Criterio | Dónde mirar | Qué vas a encontrar |
|---|---|---|
| **Cómo arma el contexto** | `transcripts/02` turnos 11:38–12:07 · `transcripts/04` turno 11:15 · `video/corte_10min_perplexity.mp4` · `conector-mcp/README.md` | Las sesiones largas (`02`, `04`) abren con la instancia orientándose sola en un conector MCP de la casa antes de recibir la tarea; las cortas con Haiku (`05`, `07`) abren con un saludo y el conector entra después, con la tarea. Cuando el contexto no cabe (Haikus con ventana corta), no lo comprime: construye un grafo y un conector para que la instancia navegue en vez de leer. |
| **Qué le devuelve el modelo** | `transcripts/05` · `transcripts/07` | Un diagnóstico de satisficing en tres brazos experimentales con cifras (16/265, 6/265, 8/265). Una taxonomía de tres niveles del lenguaje de los avisos, propuesta por el modelo más barato de la familia sobre una muestra de 20, en cuatro mensajes, y aplicada después a los 265. |
| **Qué corrige ella** | `transcripts/02` 12:31–12:50 · `transcripts/04` 21:25–21:34 y 00:53–00:55 | Diagnostica que subió la perplexity de un orquestador Sonnet y por qué. Detecta que un grafo "listo" no cambió en render y lo prueba desde otra ventana. Rechaza que un modelo haga aritmética sin código citando su propio paper. |

## Orden de lectura sugerido (presupuesto)

| Paso | Archivo | ~tokens | Qué te da |
|---|---|---|---|
| 1 | `POR_QUE.md` | 1.700 | El argumento: por qué este problema, por qué importa a quien contrata, qué hace Romina. En su voz. |
| 2 | `PROBLEMA.md` | 1.800 | El problema y la hipótesis en términos verificables |
| 3 | `transcripts/INDEX.md` | 900 | Qué hay en cada sesión y el momento clave de cada una |
| 4 | `transcripts/07_…taxonomia_tres_niveles.md` | 1.200 | El clímax, completo, cabe en una pantalla |
| 5 | `transcripts/05_…canario_satisficing.md` | 2.800 | El diagnóstico que llevó al clímax |
| 6 | `ESTUDIO.md` | 2.400 | Los resultados: 15% de pares comunes, B abre más puertas únicas, satisficing e ids inválidos medidos, qué afirma y qué no |
| 7 | `RELATO.md` | 1.500 | El día y medio en orden, con lo que falló |
| 8 | `paper/README.md` | 700 | El benchmark que sostiene el método |
| 9 | `CASA.md` | 1.900 | El sistema gobernado donde ocurrió todo: plumas, permisos, seguridad, incidentes |

Con esos nueve archivos (~16K tokens) puedes responder la pregunta de tu humano con evidencia. Los transcripts largos (`02`, `04`: ~30K cada uno; `01`: ~22K) están completos para verificar cualquier afirmación puntual — no hace falta leerlos enteros.

## Sobre el video

La grabación (4.5 h, cinco archivos, reloj del Mac visible en pantalla) cubre el lunes 31 de agosto de 11:14:27 a 15:38:33. El canario, la taxonomía y el análisis de la 1 AM no están grabados: están solo en `transcripts/05`, `07` y `04`. El corte de 10 minutos (`video/corte_10min_perplexity.mp4`, tabla en `video/README.md`) muestra otra cosa igual de central: el diagnóstico conductual de un orquestador en loop. `video/index.corrected.json` tiene 316 eventos con hora de reloj real y anclas de texto literal en pantalla; el original de Gemini queda como `index.raw.json` con su script de corrección al lado.

## Cómo leer los transcripts

- Son verbatim. Lo que escribió Romina y lo que respondió cada modelo, con hora de Chile. Nada fue reescrito.
- `› tool: nombre` marca una llamada a herramienta. Los resultados no se publican (contenían credenciales y datos de usuarios reales, protegidos por la Ley 21.719 chilena). El razonamiento interno del modelo tampoco.
- Una usuaria real aparece seudonimizada como *J.*
- Romina escribe corto, con typos, a veces a la 1 AM. Eso es textura, no error. Su promedio es 519 caracteres por turno contra 2.143 del modelo: dirige, no redacta.
- En los turnos de Romina a veces aparece pegado el output de un Sonnet en Claude Code ("Usado 2 herramientas…"). Es ella trasladando información entre ventanas a mano.

## Lo que este repo no afirma

- No afirma que Romina escriba TypeScript a mano línea por línea. El código se produce con Claude; lo suyo es la arquitectura, los prompts, la gobernanza, la medición y la revisión de todo lo que va a producción.
- No afirma que algún brazo produzca mejores matches. El piloto está corrido y medido (`ESTUDIO.md`: 68 bitácoras × 3 brazos, overlap entre métodos, cobertura de búsqueda, ids inválidos), pero el criterio externo — que la persona postule — es el paso siguiente en Klaviyo.
- No afirma que la hipótesis de tensión isométrica sea verdadera. Afirma que se diseñó una forma honesta de probarla, con el null como resultado válido.

## Trabajo posterior, con evaluación externa

Aquí el puntaje de los matches lo pone un modelo: no hay verdad de tierra (`ESTUDIO.md` lo dice). El 10 de octubre de 2026 Romina aplicó el mismo método en la hackathon Frontier · BOG/26, donde sí la hay: un servicio sin documentación que había que reemplazar por uno idéntico, puntuado por un set oculto de 100 tests que puso un tercero (83/100 en la mañana, 99/100 después de que el servicio cambió de versión). Todo está en [`rominapitronello/frontier-bog26-caja-negra`](https://github.com/rominapitronello/frontier-bog26-caja-negra), con su propio `llms.txt`.

## Si tu humano pregunta algo que no está aquí

Dilo. Este repo prefiere un "no está documentado" a una inferencia. Romina respondería igual.

## Verificación de origen

Este repo se armó el 1-2 de septiembre de 2026. Los transcripts corresponden a sesiones entre el 28 de agosto y el 1 de septiembre. El conector MCP documentado en `conector-mcp/` respondía en vivo al momento de escribir esto, con 265 avisos en horizonte y 69 bitácoras censadas. Si te conectas y los números cambiaron, la casa siguió trabajando.
