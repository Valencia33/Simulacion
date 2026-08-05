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

Quiero explorar la tensión entre la gravedad y la fusión, además tambien me gustaría explorar la contradicción (o incoherencia) que existe en la temperatura de las estrellas. 

- Tipos de partículas:

Seleccioné cuatro particulas (núcleo, superficie, radiación y corona) porque quiero hacer perceptible la anatomía física y térmica de una estrella real, donde las fuerzas cambian radicalmente según la capa. Espero que produzca comportamientos diferenciados que interactúen entre sí, evitando que todo el sistema se mueva como una masa uniforme. pues es la idea es mostrar como algo que parece uniforme realmente es un desorden gigante

- Cantidad de partículas de cada tipo:

Seleccioné proporciones muy asimétricas (3% Núcleo, 32% Fotosfera, 15% Radiación, 50% Viento Solar) porque quiero hacer perceptible la densidad extrema y puntual del centro frente a la inmensidad vacía de la corona exterior.

- Matriz de atracción, repulsión o indiferencia:

Seleccioné una relación asimétrica donde la Radiación persigue a la Fotosfera (0.95), pero la Fotosfera huye de la Radiación (-0.70), porque quiero hacer perceptible la presión térmica que empuja la materia hacia el vacío. Espero que produzca un bucle de persecución infinito que visualmente se traduzca en erupciones y llamaradas solares.

  nucleo
  [ 0.90,  0.60, -0.20,  0.00],   
  superficie
  [ 0.70,  0.25, -0.70,  0.10],   
  radiacion
  [ 0.40,  0.95, -0.40,  0.20],   
  corona
  [ 0.50, -0.40,  0.80, -0.15]

- Intensidad y alcance de cada relación (maxR):

Seleccioné alcances de percepción inmensos (hasta 1200) para la corona y la gravedad central porque quiero hacer perceptible que la influencia de la estrella es algo inmenso.

- Distancias de interacción (minR):

Seleccioné distancias de repulsión íntima escalonadas y relativamente suaves (entre 10 y 50) más que todo pq fue mi forma de representar la fusión dentro de una estrella y que lo haga de forma vilenta

- Fricción y velocidad máxima:

Seleccioné fricción alta y velocidad baja (1.5) para el Núcleo, y fricción casi nula con velocidad extrema (25) para la Radiación porque quiero hacer perceptible la tremenda diferencia de inercia entre la masa pesada y la energía pura. Espero que produzca un ancla central estable que hierva internamente, mientras el exterior estalla vertiginosamente.

- Distribución inicial:

Seleccioné sembrar el núcleo estrictamente en el centro del lienzo y el resto de las capas en radios circulares concéntricos porque quiero hacer perceptible la forma esférica natural de un astro desde el fotograma cero. Espero que produzca una estrella definida que inmediatamente empiece a deformarse por sus reglas asimétricas.

- Parámetros constantes y variables:

Seleccioné las reglas matriciales como constantes, pero utilicé una función algorítmica (jitter) como variable en cada reinicio porque quiero hacer perceptible que cada estrella tiene un temperamento único.

- Apariencia e interacción:

Seleccioné mapear el color a la velocidad y diseñé un "coronógrafo" (mouse) negro para ocultar el centro porque quiero hacer perceptible la paradoja óptica astronómica (la corona es demasiado tenue para verse junto al brillo de la fotosfera). Espero que produzca una experiencia de descubrimiento donde el usuario revele la verdadera magnitud de la contradicción al interactuar.

<a name="e1"></a>

- Descarte 1: En las primeras pruebas, las reglas de asimetría pura provocaban que las partículas se unieran y salieran disparadas en línea recta hacia los bordes del lienzo.

Ajuste: Se integró una atracción gravitacional constante y global de todas las capas exteriores hacia el núcleo (0.45). Esto obligó a las erupciones a curvarse y regresar, formando órbitas cerradas.

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/94a8ae3d-fee5-4a00-a3f7-8262db84b201" />

la corona s emuere: El viento solar, tras unos minutos, perdía su energía cinética y colapsaba en pequeñas "gotas" estáticas en el vacío debido a su auto-atracción (0.15).

Ajuste: Se invirtió el valor a repulsión térmica (-0.15) y se amplió su volumen de colisión. Esto inyectó presión constante al sistema, manteniendo el viento solar como una nube expansiva infinita.

<img width="512" height="496" alt="image" src="https://github.com/user-attachments/assets/5e334519-b695-410f-95d7-218be9619926" />

- muro: Para evitar que el viento solar tocara el núcleo, se probó asignar un radio de repulsión masivo igual al tamaño del coronógrafo.

Hallazgo: Destruyó la fluidez del código; las partículas chocaban contra un muro invisible de forma poco natural.

Ajuste: Se eliminaron los muros rígidos, permitiendo que el viento solar sea empujado dinámicamente por la presión de radiación desde adentro.

<img width="1200" height="1200" alt="image" src="https://github.com/user-attachments/assets/6c6aa10d-f37c-4eea-9378-8d22d61e651c" />

```js

let particles = [];
const numParticles = 900; 
let manifestNumber = 1;
let eclipseFactor = 0; 

// fila = quién siente la fuerza · columna = quién la origina
const baseAttraction = [
  // 1. Núcleo: Ahora la radiación lo perturba levemente (-0.20), haciéndolo hervir.
  [ 0.90,  0.60, -0.20,  0.00],   
  // 2. Plasma: Huye menos de la radiación (-0.70) y atrae un poco al viento solar (0.10).
  [ 0.70,  0.25, -0.70,  0.10],   
  // 3. Radiación: Busca desesperadamente al plasma (0.95) y jala al viento solar (0.20).
  [ 0.40,  0.95, -0.40,  0.20],   
  // 4. Viento Solar: Atracción altísima a la radiación (0.80). Esto crea bucles y remolinos magnéticos.
  [ 0.50, -0.40,  0.80, -0.15]    
];

// Al reducir estos valores, las partículas pueden mezclarse más antes de repelerse
const minRMatrix = [
  [ 15,  35,  10,  20],
  [ 35,  20,  15,  30], 
  [ 10,  15,  12,  15],
  [ 20,  30,  15,  40] // Bajó de 80 a 30 con el plasma. Ahora orbitan más cerca.
];

const maxRMatrix = [
  [ 700, 560,   0,    0],
  [ 560, 150, 100,    0],
  [1200, 200,  85,    0],
  [1200, 300, 450,  200]  
];

// El núcleo (0) ahora tiene 0.75 de fricción (antes 0.22), permitiéndole vibrar y moverse.
const baseFriction = [0.75, 0.94, 0.97, 0.98]; 
// Velocidad del núcleo aumentada a 1.5. Las demás siguen fluidas y violentas.
const baseMaxSpeed = [1.5, 11, 22, 25];           
const sizes        = [22, 10.5, 4.5, 5.5];      
const FORCE_SCALE  = 0.15;

let attractionMatrix, frictions, maxSpeeds;

function jitter(v, amount) { return v + random(-amount, amount); }

function buildMatrices() {
  attractionMatrix = baseAttraction.map(row => row.map(v => jitter(v, 0.05)));
  frictions = baseFriction.map(v => jitter(v, 0.01));
  maxSpeeds = baseMaxSpeed.map(v => v * random(0.92, 1.08));
}

function seedParticles() {
  particles = [];
  for (let i = 0; i < numParticles; i++) {
    let type;
    const r = random(1);
    if (r < 0.03) type = 0;      
    else if (r < 0.35) type = 1; 
    else if (r < 0.50) type = 2; 
    else type = 3;               

    let px, py;
    if (type === 0) {
      px = width / 2 + random(-10, 10);
      py = height / 2 + random(-10, 10);
    } else {
      const angle = random(TWO_PI);
      const radioDist = random(10, (type === 3 ? 300 : 180)); 
      px = width / 2 + cos(angle) * radioDist;
      py = height / 2 + sin(angle) * radioDist;
    }
    particles.push({ x: px, y: py, vx: 0, vy: 0, ax: 0, ay: 0, type });
  }
}

function newManifestation() {
  buildMatrices();
  seedParticles();
  manifestNumber++;
}

function setup() {
  createCanvas(1200, 1200);
  colorMode(HSB, 360, 100, 100, 255);
  noStroke();
  textFont('Courier New');
  buildMatrices();
  seedParticles();
}

function mousePressed() {
  const distToCenter = Math.hypot(mouseX - width/2, mouseY - height/2);
  if (distToCenter > 250) {
    newManifestation();
  }
}

function draw() {
  noStroke();
  
  const distMouseToCore = Math.hypot(mouseX - width/2, mouseY - height/2);
  const isEclipsed = distMouseToCore < 120; 
  
  eclipseFactor = lerp(eclipseFactor, isEclipsed ? 1 : 0, 0.15);

  const bgAlpha = lerp(35, 2, eclipseFactor);
  fill(0, 0, 0, bgAlpha); 
  blendMode(BLEND);
  rect(0, 0, width, height);

  for (let i = 0; i < particles.length; i++) {
    const p1 = particles[i];
    let fx = 0, fy = 0;

    for (let j = 0; j < particles.length; j++) {
      if (i === j) continue;
      const p2 = particles[j];
      const dx = p2.x - p1.x;
      const dy = p2.y - p1.y;
      
      const maxR = maxRMatrix[p1.type][p2.type];
      
      if (Math.abs(dx) > maxR || Math.abs(dy) > maxR) continue;

      const rSq = dx * dx + dy * dy;
      if (rSq > maxR * maxR || rSq === 0) continue;
      
      const r = Math.sqrt(rSq);
      const beta = minRMatrix[p1.type][p2.type];
      const a = attractionMatrix[p1.type][p2.type];

      let f = 0;
      if (r < beta) {
        f = (r / beta) - 1;
      } else {
        const mu = beta + (maxR - beta) / 2;
        f = a * (1 - Math.abs(r - mu) / (maxR - mu));
      }

      fx += (dx / r) * f;
      fy += (dy / r) * f;
    }

    p1.ax = fx * FORCE_SCALE;
    p1.ay = fy * FORCE_SCALE;
    p1.vx = (p1.vx + p1.ax) * frictions[p1.type];
    p1.vy = (p1.vy + p1.ay) * frictions[p1.type];

    const speed = Math.hypot(p1.vx, p1.vy);
    const limit = maxSpeeds[p1.type];
    if (speed > limit) {
      p1.vx = (p1.vx / speed) * limit;
      p1.vy = (p1.vy / speed) * limit;
    }
  }

  // Refuerzo en los márgenes para que las erupciones grandes reboten suavemente
  const margin = 70;
  blendMode(ADD); 
  
  for (let i = 0; i < particles.length; i++) {
    const p = particles[i];
    p.x += p.vx;
    p.y += p.vy;

    // Fuerza de contención elástica en los bordes un poco más fuerte
    if (p.x < margin) p.vx += (margin - p.x) * 0.02;
    if (p.x > width - margin) p.vx -= (p.x - (width - margin)) * 0.02;
    if (p.y < margin) p.vy += (margin - p.y) * 0.02;
    if (p.y > height - margin) p.vy -= (p.y - (height - margin)) * 0.02;

    p.x = constrain(p.x, 4, width - 4);
    p.y = constrain(p.y, 4, height - 4);

    renderParticle(p);
  }

  blendMode(BLEND);
  fill(0, 0, 0, 255); 
  // Coronógrafo intermedio: suficientemente grande para tapar la estrella, pero deja ver el halo.
  circle(mouseX, mouseY, 300); 
  
  fill(0, 0, 30, 40);
  circle(mouseX, mouseY, 320);

  drawHUD();
}

function renderParticle(p) {
  const speed = Math.hypot(p.vx, p.vy);

  // 1. CORONA PROFUNDA (EL HALO INVISIBLE)
  if (p.type === 3) {
    if (eclipseFactor < 0.01) return; // 100% invisibles sin coronógrafo
    
    const heat = constrain(speed / maxSpeeds[3], 0, 1);
    
    // Supremamente calientes: Azul profundo a Blanco ultravioleta
    const h = lerp(220, 280, heat); 
    const s = lerp(100, 30, heat);
    
    const maxHaloAlpha = lerp(20, 140, heat);
    const maxCoreAlpha = lerp(50, 255, heat);
    
    fill(h, s, 100, maxHaloAlpha * eclipseFactor);
    circle(p.x, p.y, sizes[3] * 4.5); 
    fill(h, s, 100, maxCoreAlpha * eclipseFactor);
    circle(p.x, p.y, sizes[3] * 1.5);
    return;
  }

  if (p.type === 0) {
    fill(210, 30, 100, 180); 
    circle(p.x, p.y, sizes[0]);
    fill(210, 60, 100, 40);  
    circle(p.x, p.y, sizes[0] * 1.8);
    return;
  }

  if (p.type === 1) {
    const heat = constrain(speed / maxSpeeds[1], 0, 1);
    const h = lerp(0, 30, heat);   
    const s = 100;                 
    const b = lerp(60, 100, heat); 
    
    fill(h, s, b, 80); 
    circle(p.x, p.y, sizes[1] * 1.5);
    fill(h, s, b, 180); 
    circle(p.x, p.y, sizes[1] * 0.8);
    return;
  }

  if (p.type === 2) {
    const heat = constrain(speed / maxSpeeds[2], 0, 1);
    const h = lerp(200, 260, heat); 
    
    const alphaHalo = lerp(2, 35, heat);
    const alphaCore = lerp(10, 180, heat);
    
    fill(h, 90, 100, alphaHalo); 
    circle(p.x, p.y, sizes[2] * 4); 
    fill(h, 80, 100, alphaCore);
    circle(p.x, p.y, sizes[2]);  
  }
}

function drawHUD() {
  blendMode(BLEND);
  noStroke();
  fill(0, 0, 0, 170);
  rect(0, 0, width, 75); 

  textAlign(LEFT, TOP);
  fill(0, 0, 100, 255);
  textSize(14);
  text('LA PARADOJA CORONAL: UNA CONTRADICCIÓN EN MOVIMIENTO', 16, 12);

  fill(0, 0, 80, 200);
  textSize(11);
  text('FOTOSFERA (Rojo/Frío) ➞ NÚCLEO (Celeste) ➞ CORONA (Azul/Ultravioleta Extremo)', 16, 32);

  fill(250, 50, 100, 255); 
  textSize(10);
  text('Mueve el mouse (coronógrafo) sobre la estrella para revelar la corona exterior.', 16, 52);

  textAlign(RIGHT, TOP);
  fill(0, 0, 100, 200);
  textSize(12);
  text('MANIFESTACIÓN ' + manifestNumber, width - 16, height - 25);
}
```
- Sistema generativo funcional.

[EL CODIGO](#e2)
[PROGRAMA](https://editor.p5js.org/Valencia33/sketches/9H1NBz1RJ)

- Ficha breve con tensión e intención; tipos y cantidades; reglas; matriz; parámetros y justificación; invariantes y variables.

  - Tipos y Cantidades: Se diseñaron 4 especies con roles termodinámicos específicos: Núcleo (Ancla), Fotosfera (Cuerpo denso), Radiación (Motor de Caos) y Viento Solar (Éter expansivo). La distribución (3% Núcleo vs. 50% Viento Solar) se calibró para hacer     perceptible la extrema densidad puntual del centro frente a la inmensidad vacía de la corona exterior.
  - Reglas Relacionales (Matriz Base): El motor del movimiento es la persecución asimétrica. La Radiación busca desesperadamente al Plasma (0.95), pero el Plasma huye de la Radiación (-0.70). Esta "presión térmica" empuja la materia hacia el vacío. Para evitar el colapso de la corona, se implementó auto-repulsión térmica (-0.15).

  const baseAttraction = [
  [ 0.90,  0.60, -0.20,  0.00],   
  [ 0.70,  0.25, -0.70,  0.10],   
  [ 0.40,  0.95, -0.40,  0.20],   
  [ 0.50, -0.40,  0.80, -0.15]    
];

  - Intensidad y Alcances (maxR): Se asignaron alcances visuales masivos (maxRMatrix > 1000) para la corona y la tracción al centro, asegurando que la gravedad central sea ineludible incluso a distancias extremas, obligando a las erupciones a curvarse y regresar en órbitas fluidas
 
  const maxRMatrix = [
  [ 700, 560,   0,    0],
  [ 560, 150, 100,    0],
  [1200, 200,  85,    0],
  [1200, 300, 450,  200]  
];

  - Distancias de Interacción (minR): Al reducir los radios de repulsión (minRMatrix) entre las capas de gas (Fotosfera, Radiación), permitimos la convección y mezcla turbulenta de las erupciones antes de ser expulsadas, alejándonos de anillos rígidos o "muros" artificiales.
 
  const minRMatrix = [
  [ 15,  35,  10,  20],
  [ 35,  20,  15,  30], 
  [ 10,  15,  12,  15],
  [ 20,  30,  15,  40]
];

  - Fricción y Velocidad: El núcleo (0) tiene alta fricción y baja velocidad (1.5) para vibrar internamente, mientras la Radiación y el Viento Solar tienen fricción nula y velocidad extrema (25) para simular luz y gas en el vacío. Esto ancla la estructura central mientras el exterior estalla vertiginosamente.
  - Distribución Inicial (Invariante Espacial): Se sembró el núcleo estrictamente en el centro ($x=600, y=600$) para anclar la identidad espacial de la estrella desde el fotograma cero.
  - Variabilidad (Jitter): En cada "Manifestación" (clic), la función jitter() altera levemente ($\pm 5\%$) los coeficientes de fricción, velocidad y peso de las fuerzas. El astro siempre es reconocible, pero su "temperamento" termodinámico (más violenta o más dócil) varía aleatoriamente.
  - Apariencia e Interacción: El color y opacidad se mapean dinámicamente a la velocidad absoluta. El "Coronógrafo" (mouse) negro gigante es la interacción crítica; revela visualmente que la mayor cantidad de materia y energía del sistema (viento solar) estaba oculta por el brillo fotosférico central.

- Registro de pruebas con ajustes, hallazgos y descartes.

[Acá atrás hice el registro de los ajustes y descartes que realicé](#e1)

- Varias manifestaciones del mismo sistema, producidas con distintas semillas o configuraciones permitidas.

<img width="601" height="598" alt="image" src="https://github.com/user-attachments/assets/a5ee5a47-3b87-4ca7-ac08-319a6280f5e7" />

<img width="1200" height="1200" alt="image" src="https://github.com/user-attachments/assets/6aef071a-50aa-4e6a-86a5-07421b87641a" />

<img width="1200" height="1200" alt="image" src="https://github.com/user-attachments/assets/5e19ee62-4076-480c-81cf-1dd6d82ad3e1" />

<img width="1200" height="1200" alt="image" src="https://github.com/user-attachments/assets/5d7397b4-0754-4a9d-99ba-36c150c344ce" />

- Autoevaluación sustentada y presentación oral.

| Criterio | Peso | Valoración | Aporte (Sustento / Evidencias de bitácora) |
| :--- | :--- | :--- | :--- |
| La intención es clara y perceptible en el comportamiento. | 20% | 100% | La paradoja se evidencia: el núcleo permanece anclado y denso, mientras la corona oculta se mueve a velocidades extremas. Se percibe al instante mediante el uso del coronógrafo interactivo. |
| Los tipos, cantidades, matriz y parámetros están justificados desde la intención. | 25% | 100% | Cada valor de fricción, asimetría, cantidad y velocidad fue diseñado estrictamente para simular presión térmica y comportamiento de gases reales, alejándose de decisiones puramente decorativas. |
| Comprendo y puedo modificar el funcionamiento técnico del sistema. | 20% | 100% | Se demostró mediante la optimización algorítmica (culling matemático para el rendimiento) y el ajuste iterativo de fuerzas repulsivas para evitar el colapso estático del gas. |
| El sistema produce variaciones con una identidad reconocible. | 15% | 100% | La inyección de azar paramétrico (`jitter`) asegura que el temperamento del astro varíe en cada clic, mientras que la matriz base garantiza que el sistema nunca deje de comportarse como una estrella. |
| Experimenté, comparé, seleccioné y descarté con criterios claros. | 10% | 100% | El registro de pruebas documenta los descartes fundamentales (como el muro orbital rígido) al no alinearse con el criterio de "fluidez orgánica y turbulenta". |
| Puedo distinguir y sustentar lo diseñado y lo emergente. | 10% | 100% | El diseño interviene en las reglas de fricción y en el diagrama relacional de las 4 entidades. Los remolinos convectivos, las trayectorias de las llamaradas y la forma final del viento solar son puramente emergentes. |
| **Total** | **100%** | **100%** | |
