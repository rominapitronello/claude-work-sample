# Auditoría externa de un producto en producción

*12 de septiembre de 2026. Cinco corridas sobre Mappa, una plataforma comercial de selección por análisis de voz, hechas desde la silla de la usuaria, sin acceso al sistema.*

Este documento no es una denuncia. Es una demostración de método: qué se puede afirmar sobre un sistema cerrado desde afuera, con qué evidencia, y dónde exactamente está la línea que no se puede cruzar sin acceso al servidor.

---

## Perímetro

Todo lo que sigue se hizo dentro de estos límites, y conviene declararlos antes que los hallazgos:

- Cuenta propia, voz propia, producto público en producción.
- Sin credenciales ajenas, sin acceso no autorizado, sin tocar infraestructura.
- Sin datos de terceros: ningún otro usuario aparece en este material.
- Los criterios de evaluación se escribieron antes de la primera corrida.
- El proveedor fue informado del hallazgo antes de esta publicación.

Un producto en producción, usado como usuaria, es superficie legítima de estudio. Lo que hace legítima la lectura no es el permiso: es el perímetro.

## Qué mide Mappa, según Mappa

La plataforma declara extraer más de 100.000 marcadores vocales de una muestra corta de voz y mapearlos a 75 rasgos conductuales. Su comunicado de la ronda semilla nombra los rasgos acústicos —variabilidad de pitch, velocidad del habla— y también los léxicos: uso de verbos, densidad de sustantivos, marcadores de primera persona. Su página de tecnología afirma que la lectura sale de la voz.

Esas dos familias de rasgos se pueden separar desde afuera, y eso es lo que hace este experimento.

## Método

**Estímulo.** Un texto fijo de 56 palabras en español, leído verbatim en las cinco corridas:

> Diseñé un instrumento para medir aprendizaje en faena. Definí los criterios, escribí las preguntas y probé la versión inicial con sesenta trabajadores. Corregí los ítems que no discriminaban. Después construí el pipeline que procesa las respuestas y verifiqué cada salida contra el código. Entrego resultados cada semana y ajusto el método cuando los datos lo piden.

**Condiciones.** Misma pieza, misma distancia al micrófono, misma sesión. Cuatro corridas en teléfono, una en computador. Una lectura deliberadamente más lenta; el resto con la misma entrega.

**Criterio, fijado antes.** Un informe cuenta como distinto si una etiqueta de rasgo aparece en una corrida y no en otra, o si un valor numérico se mueve. La prosa narrativa se excluyó de la comparación por diseño: un LLM que escribe dos veces el mismo contenido lo va a frasear distinto, y contar eso como hallazgo sería trampa. Solo se comparan etiquetas y números.

## Observaciones

### 1. Dos capas, una estable y otra no

La sección que describe cómo piensa y actúa la persona recuperó de forma confiable el contenido del texto en las cinco corridas: criterios, piloto, ítems que no discriminan, sesenta trabajadores, pipeline, verificación contra código, cadencia semanal.

La sección que describe dónde la persona rinde mejor devolvió cinco perfiles ocupacionales distintos para la misma persona y el mismo texto:

| Corrida | Perfil devuelto |
|---|---|
| 1 | Ingeniería backend: logs, métricas, salidas de test reproducibles, hooks de depuración |
| 2 | Operaciones de contenido bilingüe: cadencia de publicación, plantillas, QA, material fuente en dos idiomas |
| 3 | Estándares editoriales: criterios de aceptación, cadencia de publicación, expectativas bilingües |
| 4 | Autonomía sobre herramientas de IA, con socios en producto y marketing |
| 5 | Ejecución de procesos: playbooks, traspasos estructurados, herramientas que premian la precisión |

El texto no menciona idiomas, publicación, trabajo editorial, marketing ni selección de herramientas. Describe la construcción de un instrumento de medición para trabajadores de una faena industrial.

La sección sobre cómo colabora la persona también se invirtió: de *no vende calidez, colaboración transaccional* en la primera corrida a *lo bastante cálida para suavizar los traspasos* en la tercera, con la entrega constante.

### 2. La telemetría no responde al estímulo

La pantalla de análisis reporta fluidez, velocidad, titubeo y relación señal-ruido. Los valores finales fueron idénticos en todas las corridas —**4,6 · 142 wpm · titubeo 0,7 · S/N 8,2**— en dos dispositivos con micrófonos distintos y también en la lectura deliberadamente más lenta, donde 142 palabras por minuto no es consistente con lo que se habló.

Los valores intermedios sí varían durante la carga (se observó 4,2 · 130 · 1,3 · 6,4 a mitad de animación) y convergen siempre a los mismos cuatro. La trayectoria simula una estimación progresiva; el destino no cambia.

Esos cuatro valores no reaparecen en ninguna parte del informe entregado.

### 3. El registro de detección es fijo

Las cinco corridas mostraron los mismos tres eventos en los mismos tres segundos: huella vocal anclada en 0:03 con 97% de confianza, una triangulación a *craft & mentorship* en 0:13, y borrador listo en 0:21. La lectura lenta, que desplazó la posición de cada palabra en el audio, no los desplazó. El texto no contiene nada sobre oficio ni mentoría.

### 4. Dos fuentes, una declarada

Una corrida mostró **"Reading your LinkedIn"** durante la composición del informe. La página 2 del mismo informe afirma que las tres lecturas provienen de una sola respuesta de 30 segundos. Ambas afirmaciones se le muestran al mismo usuario con minutos de diferencia.

Eso explicaría contenido sin anclaje en el audio: las referencias a bilingüismo, por ejemplo, en una sesión donde nunca se habló inglés ni se mencionaron idiomas.

### 5. La paráfrasis cruzada de idioma implica transcripción

El estímulo es español; los informes salen en inglés y recuperan contenido específico del texto. Eso no se produce desde pitch, jitter o estructura de pausas. El propio aviso de empleo que la empresa tiene publicado para un ingeniero senior de ML nombra a Deepgram, así que la existencia de una capa de reconocimiento de habla no está en discusión. Lo que está en discusión es que el informe le diga al usuario que su lectura viene de la voz.

### 6. El usuario no puede verificar nada de esto

La generación de perfil está disponible una sola vez por cuenta. Con el mapa ya creado, la corrida no se repite. Cualquiera sea la razón de ese límite, su efecto es que ningún candidato está en posición de observar lo que se observó acá. La inestabilidad no es sutil: es inobservable desde la silla del usuario.

## Dónde está la línea

Desde afuera se puede afirmar lo que se ve: que el mismo texto produjo cinco perfiles ocupacionales distintos, que cuatro valores no se movieron, que dos afirmaciones del producto se contradicen entre sí.

No se puede afirmar la causa. Si la telemetría está escrita en el front-end o si se calcula y se descarta, si el registro de detección es decorado o una animación con curva fija, si la consulta a LinkedIn es parte del pipeline o un componente huérfano: eso requiere logs.

Quien tiene los logs puede resolverlo mirando cinco cosas: los informes generados para una cuenta en un día contra el transcripto almacenado, si los transcriptos son casi idénticos entre corridas, de dónde salen los cuatro valores, si los timestamps derivan del audio, y si la composición del informe consulta el perfil público del usuario.

Distinguir lo que se observa de lo que se infiere no es una cortesía: es lo que hace que la parte observada aguante.

## Limitaciones

Un sujeto, un texto, un día. Cinco corridas no independientes: la cuenta arrastra estado entre ellas, así que esto se parece más a una cadena que a cinco tiradas. No hay forma de enviar dos veces el mismo archivo de audio, porque la grabación ocurre dentro de la aplicación, de modo que las corridas difieren en lo que varíe entre dos lecturas del mismo texto por la misma persona. El efecto de la velocidad del habla no queda establecido: hubo una sola corrida lenta, y una corrida no separa un efecto de tempo de la varianza que ya existe con entrega constante.

Ninguna de estas limitaciones afecta las observaciones 2, 3 y 4, que tratan sobre valores y cadenas de texto que no variaron en absoluto.

## Qué demuestra este documento y qué no

**Demuestra** que un sistema cerrado se puede caracterizar desde afuera con diseño en vez de acceso: fijando el estímulo, fijando el criterio antes de mirar, y separando las capas por lo que cada una hace con el mismo input.

**No demuestra** que el producto sea malo, ni que alguien haya actuado de mala fe, ni que estos resultados se repliquen con otras voces, otros textos u otras cuentas. Con un sujeto, no se puede.

**No es** una recomendación sobre qué hacer con Mappa. Esa decisión es de quien la contrata.

---

Romina Pitronello · [pasaelfiltro.cl](https://pasaelfiltro.cl)
