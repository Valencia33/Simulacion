# UNIDAD 4: SISTEMAS DE PARTÍCULAS

## Desarrollo de concepto

Para la presentación, la verdad es que desde el principio decidí descartar el modelo clásico de sistemas de partículas. Para mí el relevo generacional no es borrar algo viejo y poner algo nuevo, es trabajar juntos y cambiar el entorno.

Me inspiré en el crecimiento de las redes de los honguitos (micelio). Construí un ecosistema fijo de 140 agentes que NUNCA desaparecen. El 40% son los de experiencia, que son más gruesos y lentos para sostener la red, y el 60% son los jóvenes, que son delgados y rápidos. El sistema evoluciona y se adapta al texto, nunca se reinicia con cada diapositiva.

## Registro de pruebas y descartes

1.) 

El problema inicial era que el código base posicionaba las partículas usando formas muy estrictas. Entonces programé un sistema distinto usando un campo de flujo (Curl Noise 2D). Ahora el movimiento ya no se ve forzado, fluye mucho más y de verdad parecen microorganismos buscando expandirse.

2.) 

Para simular crecimiento real, hice que los agentes dejaran un rastro permanente en el canvas. El tema es que esto saturaba la pantalla rapidísimo y arruinaba por completo la legibilidad del guion. 
Para arreglar eso hice tres cosas: primero, le metí un desvanecimiento súper lento con `destination-out` para que no sature. Segundo, puse un gradiente oscuro detrás del texto para que se lea siempre. Y por último, programé una fuerza que empuja a los agentes lejos del texto, así lo esquivan LITERALMENTE.

3.) 

Faltaba inmersión y demostrar que el ecosistema estaba vivo. Añadí un efecto parallax (calculando la posición del mouse y pasándola por un lerp) para separar el fondo, el texto y las partículas en tres planos de profundidad.
Además, le puse una fuerza de repulsión volumétrica al cursor. Si pasas el mouse por encima, las partículas se apartan de forma natural pero sin romper los resortes que las unen.

## Matriz de parámetros y gramática visual

Saqué los parámetros físicos directo de la narrativa del guion, no fue al azar:

- **gravity (Convocatoria):** Fórum como fuerza de atracción. Hacen steering hacia el centro (o hacia tres polos cuando habla de Academia + Industria + Ciudad).
- **clumping (Aislamiento):** Separa a los agentes en dos masas dependiendo estrictamente de a qué generación pertenecen.
- **elasticity (Confianza):** Define el umbral para conectarse, la rigidez del resorte entre partículas y cuántos enlaces máximos puede sostener cada una.
- **exploration (Rutas nuevas):** La búsqueda de nuevas rutas. Las nuevas generaciones lo aplican al 100% y la experiencia solo al 45%, se mueven muy distinto.
- **intensity (Energía):** Controla la velocidad global de la simulación.

## El argumento central en código

Para mí la parte más importante del código está en la función `buildLinks()`. Ahí se demuestra la relación:

- Con confianza 0.00, no hay ni un solo enlace.
- Con confianza 0.10, empiezan a aparecer enlaces, pero el 100% son entre generaciones distintas. Ninguno entre iguales.
- Solo a partir de confianza 0.48 empiezan a formarse enlaces entre agentes de la misma generación.

La tesis de la charla está ahí metida: la confianza se teje primero en la diversidad.

También programé un panel de debug (se activa con la tecla D) que muestra en tiempo real cómo cambian los cinco parámetros físicos, los fps, y la cantidad de enlaces cruzados vs normales. Con eso puedo demostrar en vivo en la sustentación que lo que pasa en la pantalla es pura matemática y física, no una animación pregrabada.

Y sobre la interacción con el mouse: no lo puse solo de adorno. Quería probar que el sistema está vivo. Un auditorio vacío no reacciona a nada, pero una comunidad sí. El mouse es un estímulo externo, y en vez de romperse o chocar, las partículas se acomodan y lo esquivan, sin soltar los resortes de confianza que las unen.
