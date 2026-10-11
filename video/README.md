# Video

Grabación de pantalla del **lunes 31 de agosto de 2026, 11:14:27 → 15:38:33 hora Chile**, en cinco archivos casi contiguos (hueco de 22 s entre el 1 y el 2; solapes de 59, 65 y 102 s entre los siguientes). Sin narración: Romina trabaja en silencio y escribiendo; la pantalla es el guion. El reloj del Mac es visible arriba a la derecha en todo momento — sirve para verificar cualquier afirmación de este repo contra la pantalla.

**Cubre:** la sesión con el Fable desde su apertura, el índice del PR con un Haiku, el Sonnet orquestador en loop y su diagnóstico, las reglas del cazador, el problema de contexto de los Haikus, la caída de ChatGPT y el conector MCP construido y desplegado en cámara. **No cubre** la noche del 31: el canario (22:19), la taxonomía de tres niveles (22:49) ni el "contra código" de la 1 AM. Eso está solo en `../transcripts/05`, `07` y `04`, en texto, completo.

## El corte de 10 minutos

**`corte_10min_perplexity.mp4`** — 10:31, en esta carpeta. Lunes 31, 12:30–12:41. Un Sonnet en Claude Code, encargado de orquestar una brigada de Haikus para leer 57 avisos, lleva veinte minutos pensando en círculos.

| Minuto del corte | Reloj | Qué pasa | Criterio |
|---|---|---|---|
| 00:00 | 12:30 | Romina viene de auditar a mano las trazas de razonamiento del Sonnet. Escribe a un Opus: "¿es mi idea o le subí la perplexity al Sonnet orquestador?" | contexto |
| 00:35 | 12:31 | El Opus confirma el bucle de indecisión y propone reemplazar el framework por un `for` con `try/catch` | devuelve |
| 01:50 | 12:32 | Segunda opinión: pega el output del Sonnet y pregunta "mm tengo mis dudas, ¿cómo lo ves tú?" | contexto |
| 02:35–05:00 | 12:33–12:35 | Redacta la instrucción: separar lo determinístico (cómo entregan los Haikus) de lo que es juicio (cómo el aviso presenta tensión); código listo; blindar contra alucinaciones | corrige |
| 05:45 | 12:37 | Revisa el desglose del Opus: entropía determinística (bugs) vs entropía de juicio (la divergencia 2.7×) | devuelve |
| 06:35 | 12:38 | Escribe su hipótesis: el subagente percibió una capa de supervisión inesperada y leyó desconfianza — vectores relacionales, geometría del modelo | corrige |
| 09:53 | 12:40 | El Opus, tras 31 s de razonamiento: "creo que tu hipótesis es plausible y no estás sobreinterpretando" | devuelve |
| 10:31 | 12:41 | Observa la correlación con el cambio de idioma en el prompting | corrige |

Texto de la misma escena: `../transcripts/02`, turnos 12:31 a 12:50. Recorte sin edición interna, del archivo 2 (minuto 18:42 a 29:13), recodificado a 30 fps sin audio; el original es 60 fps.

## Segunda ventana, si sobran doce minutos

**Archivo 4, minuto 13:44 → 25:45** (14:15–14:28). ChatGPT se cae en medio de una revisión adversarial con Sol; Romina pivota al Fable y le pide el conector MCP; el Fable lo diseña, despliega la edge function y prueba `tension_grafo_bitacoras` en vivo; Romina abre el mapa público, navega los nodos, y escribe: "es raro porque no lo veo en el mapa". El conector estaba desplegado; el render no había cambiado. Texto: `../transcripts/04`, 14:17 en adelante.

## Los cinco archivos

| # | Archivo | Reloj (inicio) | Duración | Enlace |
|---|---|---|---|---|
| 1 | `zesty_session_01_0000-0057.mov` | 11:14:27 | 57:06 | https://drive.google.com/file/d/1xwa-TUQB31dMR4X_EwhIGo4BiostO8KN/view |
| 2 | `zesty_session_01_0057-0150.mov` | 12:11:55 | 53:32 | https://drive.google.com/file/d/1rsdWOn1QwRguR-aqBCUHpMUXDm7EdsAO/view |
| 3 | `zesty_session_01_0149-0248.mov` | 13:04:28 | 59:02 | https://drive.google.com/file/d/1uBleoWpNdfrXlmiLEtCW0q5V29sZa_BD/view |
| 4 | `zesty_session_01_0246-0343.mov` | 14:02:25 | 56:37 | https://drive.google.com/file/d/1slOwxyfx92knh7hes6_eCRayocCNJwPc/view |
| 5 | `zesty_session_01_0343-0425.mov` | 14:57:20 | 41:13 | https://drive.google.com/file/d/1Cp2mRC8YjWvexAExnoM5uZI7xwOuqZfE/view |

1280×800, 60 fps, H.264, ~4,6 GB en total. Los nombres de archivo son aproximados al minuto; el reloj manda.

## Índice

**Usa `timestamps.corrected.md` (legible) o `index.corrected.json` (estructurado).** 316 eventos, ~1 por minuto, con la hora de reloj real y el archivo + minuto donde saltar, en orden cronológico. Cada evento conserva su `anchor`: texto literal visible en pantalla, para verificar sin mirar. Los null son null honesto.

Los originales quedan intactos: `index.raw.json` y `timestamps.md`, tal como los produjo Gemini 3.7 Flash en ventanas de 10 minutos. La corrección es determinística — `corregir_indice.py`, 40 líneas, se puede volver a correr — y existe porque Gemini procesó los archivos en otro orden y calculó los tiempos globales según ese orden. Los inicios exactos se leyeron del reloj en pantalla detectando el segundo del primer cambio de minuto en cada archivo; la primera versión del script sumaba duraciones y derivaba hasta 3,5 minutos al final, porque los archivos no son contiguos — lo encontró Sol. La equivalencia:

| Gemini dice | Archivo real | Reloj real del evento |
|---|---|---|
| clip 1 (00:00–00:57) | archivo **2** | 12:11:55 + minuto en archivo |
| clip 2 (00:57–01:50) | archivo **3** | 13:04:28 + minuto en archivo |
| clip 3 (01:50–02:49) | archivo **4** | 14:02:25 + minuto en archivo |
| clip 4 (02:49–03:31) | archivo **5** | 14:57:20 + minuto en archivo |
| clip 5 (03:43–04:25) | archivo **1** | 11:14:27 + minuto en archivo |

El `timestamp_global` del original es consistente con ese orden; el `timestamp_local` es relativo al clip en la mayoría de las ventanas y relativo a la ventana de 10 minutos en cuatro de ellas (78 eventos), así que el script usa solo el global. El "hueco 03:31–03:43" que el original declara es un artefacto: la grabación es continua. La casa prefiere corregir en público a reescribir en silencio; por eso hay dos índices y un script, no uno.
