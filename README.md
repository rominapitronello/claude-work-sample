# claude-work-sample

Un problema real de agentes de IA, resuelto de punta a punta en día y medio (28 de agosto → 1 de septiembre de 2026), con todo lo que se usó a la vista: diseño experimental, un conector MCP construido durante el trabajo, siete transcripts verbatim, lo que falló y lo que costó.

**El problema:** cómo parear a una persona con un aviso de empleo cuando lo que hizo en el pasado no describe lo que va a hacer en el futuro.

Las specs y los prompts son míos. El código lo escriben instancias de Claude y yo verifico contra el código. Quién hizo cada cosa está declarado en `CASA.md`.

Romina Pitronello · [pasaelfiltro.cl](https://pasaelfiltro.cl)

---

## No es escribir prompts

Escribir prompts lo ofrece mucha gente y es la parte corta. Lo que hago es otra cosa: construyo la gobernanza del sistema, estudio la cognición y las capacidades de los modelos, y con eso establezco perímetros de autonomía donde el modelo avanza sin que yo dictamine cada paso. Por eso los resultados no se parecen a lo que habría hecho una persona haciendo la misma tarea a mano.

---

## Un caso completo, antes de que sigas leyendo

Volumen de commits de un agente no prueba nada sobre quien lo dirige. Lo que sirve es el eslabón: esta instrucción mía → esto devolvió → esto rechacé y por qué. Uno completo, corto:

**La spec.** Tres brigadas de cazadores Haiku, una por brazo experimental, buscando matches entre 68 bitácoras y un universo de 265 avisos. La instrucción decía que buscaran matches.

**Lo que devolvieron.** Los tres brazos declararon resultados con confianza. El canario mostró la cobertura real: el brazo A profundizó en 16 avisos de 265, el B en 6, el C en 8. Encontraron un patrón temprano, generalizaron al universo completo y pararon.

**El rechazo.** No acepté los resultados. Le pasé el reporte del orquestador a un Haiku limpio, con su conector MCP, para que mirara el grafo y me dijera por qué. Su diagnóstico: *"es un problema de diseño del prompt, no de los Haikus"*. Les pedí buscar, no les puse un piso de exploración. Sin piso, el modelo optimiza por velocidad y confianza, no por cobertura.

**Lo que pasó después.** Ese piso mínimo no alcanzó a entrar al harness de esa corrida. Está declarado como tal en `ESTUDIO.md`, junto con la medición a escala: la mediana de avisos vistos fue 7–8 de 265 en los tres brazos, y 160 de 900 matches (18%) apuntan a un aviso que no existe.

El transcript completo de ese diagnóstico está en `transcripts/05`. La corrección de prompt está en `transcripts/02`, a las 12:31. La misma mecánica aparece en `transcripts/04` a las 21:25, cuando el render de un grafo entregado como listo resultó no haber cambiado nada.

Publicar la tasa de error propia antes de que la pregunten es parte del método, no un gesto.

---

## Dónde vive el trabajo, y qué se puede verificar

Este repositorio es una muestra, no el sistema. La asimetría de fechas es real y conviene decirla de entrada:

| | |
|---|---|
| Producto en operación (`PasaElFiltro/pasaelfiltro`) | **privado**. 2.260 commits y 489 pull requests desde el 9 de julio de 2026. |
| Reparto de autoría en ese repo | 1.138 commits de la cuenta de los Claude de la casa, 821 de la cuenta de un agente GPT, 280 de otra instancia, **1 mío**. |
| Este repositorio | público, creado el 1 de septiembre de 2026. |

El repo de producto es privado porque contiene datos de usuarias reales y credenciales. Eso significa que el historial de commits, que es la evidencia más directa de cómo trabajo, no es públicamente auditable. Lo que sí lo es, y está acá:

- los siete transcripts verbatim, con lo que escribí yo y lo que respondió cada modelo;
- la bitácora de ejecución que el Sonnet orquestador dejó en el PR #533 al terminar la corrida (`transcripts/claude-code/`), escrita por el modelo;
- el conector MCP con sus siete herramientas documentadas, que se puede conectar y probar;
- el estudio con sus propios errores medidos.

Si para tu decisión necesitas ver el historial privado, se coordina acceso de lectura.

---

## Qué hay acá

| Carpeta / archivo | Qué es | Para quién |
|---|---|---|
| `POR_QUE.md` | Qué es PasaElFiltro, por qué este problema, y qué hago yo que no cabe en quince minutos de pantalla. Punto de partida si eres humano. | humano |
| `LLM_START_HERE.md` | Orden de lectura con presupuesto de tokens. Si le pasas este repo a tu Claude, que parta ahí. | LLM |
| `PROBLEMA.md` | El problema, la hipótesis (tensión isométrica), el diseño experimental de tres brazos, qué se encontró. | los dos |
| `ESTUDIO.md` | Resultados de la corrida completa: 68 bitácoras × 3 brazos contra 265 avisos, computados por SQL contra la tabla. Incluye lo que salió mal y cuánto. | los dos |
| `RELATO.md` | El día y medio en orden: qué se pidió a quién, qué falló, qué se corrigió. | los dos |
| `transcripts/` | Siete sesiones con Claude (Haiku, Opus, Fable), verbatim. Índice en `transcripts/INDEX.md`. | LLM |
| `conector-mcp/` | El conector MCP construido durante el trabajo — *Tensión isométrica* — con sus siete herramientas documentadas. | conectable |
| `paper/` | El estudio preregistrado sobre variabilidad inter-instancia, enviado a *Behavior Research Methods*. El benchmark del que sale el método. | los dos |
| `CASA.md` | Lo que rodea al problema: siete plumas con permisos declarados, inspector de prompt injection, mínimo privilegio para un agente de otro proveedor, orientación separada de autorización, un incidente de costo. | los dos |
| `lab/` | El experimento de la ballena: siete modelos, un system prompt, una sonda conductual. Ocio fecundo. | LLM |
| `video/` | Corte de 10 minutos en el repo; el completo (4,5 h) en Drive, con índice corregido a hora de reloj y reloj visible en pantalla. | humano |
| `CRONOLOGIA.md` | Tabla hora ↔ ventana ↔ minuto de video. | LLM |

## Tres rutas según cuánto tiempo tengas

**Diez minutos.** `video/corte_10min_perplexity.mp4` (13 MB, en el repo). Un Sonnet orquestador lleva veinte minutos en loop; ahí se ve cómo lo diagnostico —con una hipótesis sobre su conducta, no sobre su código—, qué me devuelven dos modelos y cómo reescribo el prompt.

**Media hora leyendo.** `POR_QUE.md`, después `transcripts/07` y `transcripts/05` en ese orden, después `ESTUDIO.md` desde la sección de errores.

**Un prompt.** Pásale la URL de este repo a tu propio Claude y pregúntale qué construí, qué me devolvió y qué corregí. `LLM_START_HERE.md` está escrito para que te responda con evidencia y no con adjetivos. Si te devuelve adjetivos, eso también es información: sobre el modelo, sobre el prompt, o sobre este repo.

## Lo que no está

Credenciales, datos de usuarias reales, razonamiento interno de los modelos. Cada transcript declara en su cabecera qué se omitió y por qué. Lo que sí está no fue reescrito ni reordenado.

## Sobre el origen de este repositorio

Nació el 1 de septiembre de 2026 como respuesta a una petición concreta: veinte minutos de pantalla trabajando con Claude en un problema real. Quedó en esto por lo que dice el segundo bloque de este documento. Se publica tal cual porque el problema que resuelve no es exclusivo de quien lo pidió.

---

Romina Pitronello · [pasaelfiltro.cl](https://pasaelfiltro.cl) · [github.com/PasaElFiltro](https://github.com/PasaElFiltro)
