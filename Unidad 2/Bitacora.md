# UNIDAD 2

## Actividad 1

En este primer acercamiento al particle life (del cual, previo a ver los videos, tenía una idea muy primitiva) veo que va mucho más allá de la simulación de un par de particulas con reglas de relación. Y despues de ver los videos tengo varias ideas de referentes para el reto de diseño (no he explorado lo suficiente el concepto aún pero quiero hacer algo relacionado con el espacio).

<img width="1230" height="622" alt="image" src="https://github.com/user-attachments/assets/de51ee2c-a991-47d3-aff1-b2477a692e6b" />

<img width="1164" height="631" alt="image" src="https://github.com/user-attachments/assets/ebd82dfa-74b6-4432-9465-8d1dfdbcf938" />

## Actividad 2

Comprendo que el movimiento predeterminado de una particula está dado por x(t), x'(t) = v(t) y x''(t) = a(t) y que esa aceleración es manipulada por las fuerzas que se aplique y disminuye si existe fuerza de fricción, esto es bastante util para el comportamiento de mis particulas, pues es la base del resto de cosas que voy a construir, ya solo quedaría empezar a diseñar las reglas por las cuales se va a regir mi proyecto.

## Actividad 3

Observé los 3 videos y miré y analicé los dos ejecutables, sin embargo la que más me llamó la atención y la que pienso discutir es el tercer video, que habla de la implementacioón, la maetmatica y el código detrás de un particle life. me parece una implementación interesante, sin embargo, por lo que he visto y lo que más me asusta del proceso es el rendimiento del programa, pues si quiero mcuhas particulas voy a tener que saber como manejarlas correctamente, partiendo de esto, hace un rato leí que para optimizar este tipo de sistemas es importante dividir el espacio en cuadrantes, y que a la hora de chequear distancias solo lo hiciera con cuadrantes adyacentes al que está la particula que quiero mover.

## Actividad 4

- Intención: ¿Qué transformación, sensación, tensión o idea debe experimentar quien observa?

El equilibrio tan caótico que hay dentro de una estrella, el balance de fuerzas tan grandes que existen dentro de ella y la inmensidad de ese proceso, que es más de lo que ve.

- Entidades: ¿Qué elementos existen? Partículas, especies, campos, fronteras, memorias o señales.

Tengo planeado que existan 4 particulas, todas partes de la anatomía de una estrella las del núcleo de la estrella, la superficie de la esfera, la radiación que saca la esfera y la corona. 

- Relaciones: ¿Cómo se afectan? Atracción, repulsión, persecución, cooperación, competencia o indiferencia.

El sistema trata del equilibrio en las fuerzas y la persecusión, hay una atracción de todas las capas hacía el núcleo central y hay una repulsión entre la radiación y la superficie, simulando la fusión dentro de la estrella. Existe coperación entre la raciadión y el viento solar, lo que genera remolinos y corrientes

- Entradas: ¿Qué alimenta el sistema? Semilla, tiempo, audio, interacción, datos o decisiones del participante.

La semilla que inyecta el usuario y el uso del coronografo, pero el factor constante es el tiempo

- Reglas: ¿Cómo cambia el estado de un frame al siguiente?

en cada frame cada particula mira su radio, cada particula tiene un radio minimo y un radio max si esta debajo de la minima la repel y si esta dentro de la mazima hace la fuerza de atraccion o huida

- Invariantes: ¿Qué debe permanecer para conservar la identidad del sistema?

Las capas deben permanecer siempre intacatas, es decir las matricez de comportamiento de cada particula.

- Variabilidad: ¿Qué puede ser diferente en cada ejecución sin destruir esa identidad?

El temperamento de la estrella.

- Curaduría y reflexión: ¿Qué resultado es significativo y cuál es solo un accidente interesante?

Cuando suceden protuberancias/vientos solares 


## Actividad 5


