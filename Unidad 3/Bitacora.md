## Comandos git bash

$ git clone https://github.com/Valencia33/Unidad-3-Simulacion.git //CLONAR REPO

$ ls //VER DONDE ESTOY

$ cd Unidad-3-Simulacion/ unidad3/ //CAMBIAR DIRECTORIO

$ npm install //INSTALAR DEPENDENCIAS

$ npm run dev //ABRIR SERVER LOCAL

$ code . //ABRIR SCRIPTS

## Actividad 2

1.) ¿Qué datos representan el estado de cada partícula y dónde viven?

El estado de cada particula está representado por dos vectores, uno de velocidad y otro de posición, ambos tipos de datos viven en la GPU, mas especificamente viven en la VRAM.

2.) ¿Qué fuerzas se suman y qué ecuación o dirección representa cada una?

En mi implementación se aplican varias fuerzas eso depende de si la particula está en el circulo interno o externo, esas fuerzas son las siguientes: gravedad (Calcula un punto ideal en el radio del anillo y empuja la partícula hacia él), empuje radial (Un empuje que va desde el centro hasta las particulas para empujarlas hacia afuera), giro(una fuerza que se aplica de forma perpendicular al centro para que de la sensación de orbita), turbulencia (una capa de ruido con sen y cos en para crear ruido) y fricción, que se opone al movimiento neto para mantener bajo control el sistema.

3.) ¿Cómo pasa una fuerza a aceleración, velocidad y posición?

se usa euler semi implicito, lo que significa que de aceleración a velocidad se multiplica la fuerza total por dt y se le suma la velocidad actual y esa velocidad se limita para que no explote y todo salga volando. Y para velocidad a posición se agarra la nueva velocidad calculada y se multiplica por dt y se le suma la posición actual.

4.) ¿Cómo se dibuja el estado calculado sin volver a simularlo?

la verdad ni idea,

5.) ¿Qué parámetros puede tocar el intérprete y por qué esos?

El usuario puede tocar 3 tipos de parametros: fisicos, visuales y postprocesados, los fisicos se refierer a esos que aplican fuerzas directamente sobre las particulas, las visuales son puramente para cambiar de color las particulas y el postprocesado para jugar con los efectos de postprocesado que hay en el sistema.

<img width="1011" height="635" alt="image" src="https://github.com/user-attachments/assets/a32fd9be-47a2-4b72-a38f-93f50260e87c" />

## Actividad 3

### SCORE VISUAL

PATRONES BACANOS QUE ME ENCONTRÉ EXPERIMENTANDO:

X + C al tempo de la canción : hacen que un circulo no perfecto salte en el centro
X + SHIFT intermitente que el tempo cambie: bola con imperfecciones
C + SHIFT al tempo de la cancion: patrones cool con el ritmo

- EMPEZAR CON Z Y SHIFT PRESIONADOS HASTA EL PRIMER TIRIN.
- X + SHIFT INTERMITENTE


### FICHA DE FUERZAS Y REGISTRO PRUEBAS

### BITÁCORA IA

Lo primero que hice con la IA fue que analizara el contexto del trabajo, a partir de esto comprendió que iba a hacer el rol de asistente y que yo le iba a ordenar como hacer las cosas y donde meterlas. 

<img width="615" height="80" alt="image" src="https://github.com/user-attachments/assets/26bdd0f2-5e05-4ee5-816a-51717b2bc507" />

Siguiente utilicé como referencia los videos de NCS que tienen un visualizador que tiene una bola que pareciera que respira, pues eso era lo que quería lograr con mi interpretación, una especie de ser vivo que te observa, se estresa y está tranquilo.

por lo que el primer pass de parametros que ibamos a utilizar fue este:

```js
import * as THREE from 'three/webgpu';
import { uniform } from 'three/tsl';

// Uniforms are CPU-side values that TSL exposes to the GPU.
// Changing .value does not rebuild the compute shader.
export function createParameters() {
  return {
    dt: uniform(1 / 60),
    timeScale: uniform(1.0),
    initialSpeed: uniform(0.35),
    maxSpeed: uniform(5.0),
    boundsSize: uniform(10.0),
    particleSize: uniform(0.035),

    windEnabled: uniform(0.0),
    wind: uniform(new THREE.Vector3(0.0, 0.0, 0.0)),

    radialEnabled: uniform(1.0),
    attractor: uniform(new THREE.Vector3(0.0, 0.0, 0.0)),
    radialStrength: uniform(2.2),
    softening: uniform(0.35),

    vortexEnabled: uniform(1.0),
    vortexStrength: uniform(1.4),

    dragEnabled: uniform(1.0),
    dragCoefficient: uniform(0.12),

    // Nuevos parámetros para los atractores orbitales
    time: uniform(0.0),
    orbitRadius: uniform(3.0),
    orbitSpeed: uniform(1.5)
  };
}
```
Lo que veía hasta el momento no me gustó, puesot que aún tenía mucho ADN del proyecto base, por lo que decidí decirle que borrara todas las fuerzas que se aplicaban desde el usuario y que fueramos a crearlas desde cero. Paré y analicé la pieza, y entendí que lo mejor sería crear un diferenciador del BAJO y de los ALTOS.

<img width="680" height="345" alt="image" src="https://github.com/user-attachments/assets/70ea10af-07b9-45e9-aa4d-9cfd4352c71b" />

Como ya tenía gran parte de las fuerzas, y la IA conoce el contexto le pregunté que faltaba para completar los parametros de la unidad:

<img width="728" height="661" alt="image" src="https://github.com/user-attachments/assets/7abca3d9-4bde-4cb8-9739-0f4ae5d55a18" />

Despues de esto decidí ignorar todo lo que me dijo e irme por una tangente que no tenía absolutamente nada que ver con el trabajo pero que disfruté mucho y fue añadirle un sintetizador, seré breve. Pero busqué el tono de la canción y diseñé 5 arpegios que estuvieran en esa escala y los mapee a "a", "s", "d", "f", "g". y pasé muy bueno tocando a la par con la canción.

Por último realicé a mano un tweak para el color y le pregunté sobre las interacciones que teniamos hasta el momento.

<img width="682" height="495" alt="image" src="https://github.com/user-attachments/assets/a25aae87-531a-4713-8048-6c63a3dd3be0" />

A partir de esto, ajusté con ayuda de la IA las interacciones y su influencia en lo que ya tenía, además, le dije que agregara en el lab panel pequeñas descripciones de lo que realizaba cada cosa.

POR ÚLTIMO, le dije al parcero que buscara alguna librería o algo y añadiera efectos de post procesado, puse mis favoritos, bloom, chromatic aberration, fish eye y vignette se veía horrible entonces decidí mapear los valores de estos parametros a la barra espaciadora y como sentía que estaba corto en interacciones diseñe tres nuevas y le dije que las implementara

<img width="643" height="217" alt="image" src="https://github.com/user-attachments/assets/0dc7056e-9335-4467-83c8-047d7b282075" />

Despues de la clase del miercoles sufrí terribles noticias:

<img width="489" height="333" alt="image" src="https://github.com/user-attachments/assets/374e0a5a-3662-4322-b7b5-b501719db160" />

Jugar con la camara no me dió ningún resultado satisfactorio por lo que decidí dejar así.

### AUTOEVALUACIÓN
