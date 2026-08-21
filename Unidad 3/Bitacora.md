
# PAGINA

[hola, soy la página](https://valencia33.github.io/UNIDAD3-SIMULACION/)

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

PARAMETERS
```
import * as THREE from 'three/webgpu';
import { uniform } from 'three/tsl';

export function createParameters() {
  return {
    dt: uniform(1 / 60),
    timeScale: uniform(1.0),
    initialSpeed: uniform(0.35),
    maxSpeed: uniform(12.0),
    boundsSize: uniform(10.0),
    particleSize: uniform(0.04),

    time: uniform(0.0),

    // GRAVES (Anillo Morado)
    ringRadius: uniform(3.0),
    gravityStrength: uniform(6.0),
    swirlStrength: uniform(2.0),
    kickForce: uniform(0.0), 

    // AGUDOS (Anillo Azul)
    ring2Radius: uniform(5.0), 
    ring2Gravity: uniform(4.0), 
    highsSwirl: uniform(3.0), 
    highsTurbulence: uniform(0.0),

    // GLOBALES
    damping: uniform(0.15),
    colorPhase: uniform(0.0), // 0.0 Normal, 1.0 Mutación Galáctica

    // POST-PROCESAMIENTO
    fishEye: uniform(0.25),
    chromaticAberration: uniform(0.008), 
    bloomStrength: uniform(0.006), 
    vignette: uniform(0.85) 
  };
}
```

CREATESIMULATION
```
import * as THREE from 'three/webgpu';
import {
  Fn,
  If,
  color,
  hash,
  instanceIndex,
  instancedArray,
  max,
  mix,
  mod,
  step,
  uint,
  uv,
  vec3,
  vec4,
  sin,
  cos
} from 'three/tsl';

export function createSimulation({ renderer, scene, params, count = 131072 }) {
  const positionBuffer = instancedArray(count, 'vec3');
  const velocityBuffer = instancedArray(count, 'vec3');

  const initParticles = Fn(() => {
    const i = instanceIndex;
    const p = positionBuffer.element(i);
    const v = velocityBuffer.element(i);

    const r1 = hash(i.add(uint(11)));
    const r2 = hash(i.add(uint(23)));
    const r3 = hash(i.add(uint(37)));
    
    p.assign(vec3(r1, r2, r3).sub(0.5).mul(params.boundsSize.mul(0.45)));
    v.assign(vec3(0.0));
  })().compute(count).setName('Initialize Particles');

  const updateParticles = Fn(() => {
    const p = positionBuffer.element(instanceIndex);
    const v = velocityBuffer.element(instanceIndex);

    const dt = params.dt.mul(params.timeScale);
    const force = vec3(0.0).toVar();

    const pID = hash(instanceIndex);
    const isHigh = step(0.5, pID); 
    const isGrave = step(pID, 0.5); 

    const pXZ = p.mul(vec3(1.0, 0.0, 1.0));
    const distXZ = max(pXZ.length(), 0.1);
    const currentDir = pXZ.div(distXZ);
    const swirlDir = vec3(p.z.mul(-1.0), 0.0, p.x).normalize();

    // GRAVES 
    const ringTarget = currentDir.mul(params.ringRadius);
    const graveForce = ringTarget.sub(p).mul(params.gravityStrength);
    graveForce.addAssign(currentDir.mul(params.kickForce));
    graveForce.addAssign(swirlDir.mul(params.swirlStrength));

    // AGUDOS 
    const ring2Target = currentDir.mul(params.ring2Radius);
    const agudoForce = ring2Target.sub(p).mul(params.ring2Gravity);
    agudoForce.addAssign(swirlDir.mul(params.highsSwirl));

    const t = params.time.mul(2.0);
    const noiseForce = vec3(
      sin(p.y.mul(2.0).add(t)),
      cos(p.z.mul(2.0).sub(t)),
      sin(p.x.mul(2.0).add(t))
    );
    agudoForce.addAssign(noiseForce.mul(params.highsTurbulence));

    force.addAssign(graveForce.mul(isGrave));
    force.addAssign(agudoForce.mul(isHigh));

    force.addAssign(v.mul(params.damping).mul(-1.0));

    v.addAssign(force.mul(dt));

    const speed = v.length();
    If(speed.greaterThan(params.maxSpeed), () => {
      v.assign(v.normalize().mul(params.maxSpeed));
    });

    p.addAssign(v.mul(dt));

    const half = params.boundsSize.mul(0.5);
    p.assign(mod(p.add(half), params.boundsSize).sub(half));
  })().compute(count).setName('Update Particles');

  // RENDER: PALETA GALÁCTICA PURA
  const material = new THREE.SpriteNodeMaterial({
    blending: THREE.AdditiveBlending,
    depthWrite: false,
    transparent: true
  });

  material.positionNode = positionBuffer.toAttribute();
  material.scaleNode = params.particleSize;

  material.colorNode = Fn(() => {
    const pID = hash(instanceIndex);
    const isHigh = step(0.5, pID);

    const speed = velocityBuffer.toAttribute().length();
    const speedNorm = speed.div(params.maxSpeed).clamp(0.0, 1.0);
    
    // tColor recorre el gradiente basado en velocidad y el ID de la partícula
    const tColor = speedNorm.add(pID.mul(0.5)).mod(1.0);

    // 1. NEBULOSA (Graves): Vacío Oscuro -> Violeta -> Rosa Cósmico
    const cG1 = color('#0a001a');
    const cG2 = color('#6600ff');
    const cG3 = color('#ff0051');
    const rgbGrave = mix(
      mix(cG1, cG2, tColor.mul(2.0).clamp(0.0, 1.0)),
      cG3,
      tColor.sub(0.5).mul(2.0).clamp(0.0, 1.0)
    );

    // 2. ESTRELLAS (Agudos): Espacio Profundo -> Cyan -> Estrella Blanca
    const cA1 = color('#001569');
    const cA2 = color('#00f2ff');
    const cA3 = color('#cb82ff');
    const rgbAgudo = mix(
      mix(cA1, cA2, tColor.mul(2.0).clamp(0.0, 1.0)),
      cA3,
      tColor.sub(0.5).mul(2.0).clamp(0.0, 1.0)
    );

    // Mutación con la tecla C (Intercambia paletas)
    const finalGrave = mix(rgbGrave, rgbAgudo, params.colorPhase);
    const finalAgudo = mix(rgbAgudo, rgbGrave, params.colorPhase);

    const rgbFinal = mix(finalGrave, finalAgudo, isHigh);
    
    // Hacemos que la "nebulosa" base sea muy brillante
    const brightness = speedNorm.mul(1.5).add(0.8); 
    
    return vec4(rgbFinal.mul(brightness), 1.0);
  })();

  material.opacityNode = step(uv().xy.sub(0.5).length(), 0.5);

  const geometry = new THREE.PlaneGeometry(1, 1);
  const mesh = new THREE.InstancedMesh(geometry, material, count);
  mesh.frustumCulled = false;
  scene.add(mesh);

  function reset() {
    renderer.compute(initParticles);
  }

  function stepSimulation() {
    renderer.compute(updateParticles);
  }

  function dispose() {
    geometry.dispose();
    material.dispose();
    scene.remove(mesh);
  }

  return { count, positionBuffer, velocityBuffer, reset, stepSimulation, dispose };
}
```

MAIN
```
import * as THREE from 'three/webgpu';
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
import WebGPU from 'three/addons/capabilities/WebGPU.js';
// Importamos la trigonometría necesaria para el caleidoscopio (atan, mod, abs, cos, sin, mix)
import { Fn, uv, texture, vec2, vec3, vec4, length, max, atan, mod, abs, cos, sin, mix, uniform, float } from 'three/tsl';
import './styles.css';

import { createParameters } from './simulation/parameters.js';
import { createSimulation } from './simulation/createSimulation.js';
import { createLabPanel } from './ui/labPanel.js';

const PARTICLE_COUNT = 131072;

async function main() {
  const mount = document.querySelector('#app');

  if (!WebGPU.isAvailable()) {
    mount.appendChild(WebGPU.getErrorMessage());
    throw new Error('Este proyecto requiere WebGPU para ejecutar compute shaders.');
  }

  const scene = new THREE.Scene();
  scene.background = new THREE.Color('#050607');

  const camera = new THREE.PerspectiveCamera(50, innerWidth / innerHeight, 0.05, 100);
  camera.position.set(0, 14, 0.01); 

  const renderer = new THREE.WebGPURenderer({ antialias: true });
  renderer.setPixelRatio(Math.min(devicePixelRatio, 2));
  renderer.setSize(innerWidth, innerHeight);
  mount.appendChild(renderer.domElement);
  await renderer.init();

  const orbit = new OrbitControls(camera, renderer.domElement);
  orbit.enableDamping = true;
  orbit.target.set(0, 0, 0);

  const params = createParameters();
  // Uniforms del Caleidoscopio
  params.kaleidoscope = uniform(0.0);      // mezcla 0..1, disparada con V
  params.kaleidoSegments = uniform(6.0);   // nº de espejos / rebanadas
  params.kaleidoSpin = uniform(0.15);      // velocidad orbital del punto de muestreo
  params.kaleidoOffset = uniform(0.12);    // qué tan lejos del centro se toma la muestra

  const simulation = createSimulation({ renderer, scene, params, count: PARTICLE_COUNT });

  const axes = new THREE.AxesHelper(1.5);
  scene.add(axes);

  // SISTEMA DE POST-PROCESAMIENTO
  const renderTarget = new THREE.RenderTarget(innerWidth, innerHeight, { type: THREE.HalfFloatType });
  const postScene = new THREE.Scene();
  const postCamera = new THREE.OrthographicCamera(-1, 1, 1, -1, 0.1, 10);
  postCamera.position.z = 1; 

  const postMaterial = new THREE.MeshBasicNodeMaterial({ depthWrite: false, depthTest: false });
  const postQuad = new THREE.Mesh(new THREE.PlaneGeometry(2, 2), postMaterial);
  postScene.add(postQuad);

  const texTarget = renderTarget.texture;

  postMaterial.colorNode = Fn(() => {
    const vUv = uv();
    const centered = vUv.sub(0.5);
    const dist = length(centered);
    
    const safeDist = max(dist, 0.0001);
    const dir = centered.div(safeDist);

    const distortion = dist.mul(dist).mul(params.fishEye).add(1.0);
    const distortedUv = centered.mul(distortion).add(0.5);

    // =======================================
    // MAGIA CALEIDOSCÓPICA (Coordenadas Polares)
    // =======================================
    // Un caleidoscopio real no refleja el centro exacto de la escena (que ya es
    // simétrico por los anillos de partículas — reflejarlo ahí apenas se nota).
    // En su lugar toma una muestra DESPLAZADA del "tubo" y la hace orbitar en
    // el tiempo, como el fragmento de vidrio que cae dentro del tubo mientras
    // este gira. Eso es lo que le da vida y lo hace ver como un caleidoscopio
    // real en vez de una simetría estática y redundante.
    const orbitAngle = params.time.mul(params.kaleidoSpin);
    const orbitOffset = vec2(cos(orbitAngle), sin(orbitAngle)).mul(params.kaleidoOffset);
    const kSource = centered.add(orbitOffset);

    const angle = atan(kSource.y, kSource.x);
    const radius = length(kSource).mul(distortion);
    const segments = params.kaleidoSegments;
    const slice = float(Math.PI * 2.0).div(segments);
    
    // Convertimos el ángulo en un espejo circular
    const modAngle = mod(angle.add(Math.PI), slice);
    const symAngle = abs(modAngle.sub(slice.div(2.0))); 
    
    // Devolvemos a coordenadas Cartesianas (X, Y)
    const kCentered = vec2(cos(symAngle), sin(symAngle)).mul(radius);
    const kUv = kCentered.add(0.5);
    
    // Mezcla suave entre el UV normal distorsionado y el Caleidoscopio
    const finalUv = mix(distortedUv, kUv, params.kaleidoscope);

    // Aberración cromática usando el mapa final doblado
    const ca = params.chromaticAberration;
    const uvR = finalUv.add(dir.mul(ca));
    const uvG = finalUv;
    const uvB = finalUv.sub(dir.mul(ca));

    const r = texture(texTarget, uvR).r;
    const g = texture(texTarget, uvG).g;
    const b = texture(texTarget, uvB).b;
    const baseColor = vec3(r, g, b);

    // Bloom Exagerado
    const bRad = params.bloomStrength;
    const bRadNeg = bRad.mul(-1.0);
    
    const blur1 = texture(texTarget, finalUv.add(vec2(bRad, bRad))).rgb;
    const blur2 = texture(texTarget, finalUv.add(vec2(bRadNeg, bRad))).rgb;
    const blur3 = texture(texTarget, finalUv.add(vec2(bRad, bRadNeg))).rgb;
    const blur4 = texture(texTarget, finalUv.add(vec2(bRadNeg, bRadNeg))).rgb;
    
    const blur = blur1.add(blur2).add(blur3).add(blur4).div(4.0);
    const bloomColor = baseColor.add(blur.mul(1.5)); 

    const vignette = dist.mul(params.vignette).negate().add(1.0).clamp(0.0, 1.0);

    return vec4(bloomColor.mul(vignette).clamp(0.0, 1.0), 1.0);
  })();

  // baseState es ahora la ÚNICA fuente de verdad para los valores "base": los
  // sliders del panel escriben aquí directamente (ver ui/labPanel.js). Cada
  // frame recalculamos los params reales combinando baseState + los efectos
  // de teclado, así que las teclas de Performance ya NO dependen del modo.
  const baseState = {
    ringRadius: params.ringRadius.value,
    gravityStrength: params.gravityStrength.value,
    ring2Radius: params.ring2Radius.value,
    ring2Gravity: params.ring2Gravity.value,
    swirlStrength: params.swirlStrength.value,
    highsSwirl: params.highsSwirl.value,
    highsTurbulence: params.highsTurbulence.value,
    fishEye: params.fishEye.value,
    chromaticAberration: params.chromaticAberration.value,
    bloomStrength: params.bloomStrength.value,
    vignette: params.vignette.value,
    damping: params.damping.value
  };

  // ESTADO DE TECLAS (ya no se filtran por modo: ver keydown/keyup más abajo)
  let isSpaceDown = false;
  let isCDown = false;
  let isZDown = false;
  let isXDown = false;
  let isVDown = false;
  let isShiftDown = false;
  
  let kickProgress = 0.0;
  let colorProgress = 0.0;
  let vProgress = 0.0;

  // El ratón sigue controlando Agudos SOLO en Performance: si también lo hiciera
  // en LAB, cada movimiento del mouse pelearía con lo que acabas de ajustar
  // en los sliders. Guardamos su último valor aparte en vez de pisar el param.
  let mouseRing2Radius = null;
  let mouseHighsTurbulence = null;

  let paused = false;
  let mode = 'LAB';
  let panel;

  const applyPreset = (id) => {
    baseState.gravityStrength = 6.0;
    baseState.ring2Gravity = 4.0;
    
    if (id === 'disco') {
      baseState.ringRadius = 3.0;
      baseState.ring2Radius = 5.0;
      baseState.highsTurbulence = 0.0;
    } else if (id === 'storm') {
      baseState.ring2Radius = 8.0;
      baseState.highsTurbulence = 15.0;
      baseState.swirlStrength = 6.0;
    }
    panel?.refresh();
  };

  const setMode = (next) => {
    mode = next;
    const lab = mode === 'LAB';
    panel.setVisible(lab);
    axes.visible = lab;
    hud.innerHTML = lab
      ? '<strong>LAB</strong> · P: performance · R: reset · Espacio/Shift/Z/X/C/V funcionan aquí también'
      : '<strong>PERF:</strong> RATÓN (Agudos) · ESPACIO (Kick) · SHIFT (Slow-Mo) · Z/X (Físicas) · V (Caleidoscopio) · C (Color)';
  };

  panel = createLabPanel({
    params,
    baseState,
    onReset: () => simulation.reset(),
    onPreset: applyPreset,
    onModeChange: () => setMode(mode === 'LAB' ? 'PERFORMANCE' : 'LAB'),
    onPauseChange: () => paused = !paused
  });

  const hud = document.createElement('div');
  hud.className = 'hud';
  document.body.append(hud);
  setMode('LAB');

  addEventListener('pointermove', (event) => {
    if (mode === 'PERFORMANCE') {
      const normX = event.clientX / innerWidth;
      const normY = event.clientY / innerHeight;
      
      mouseRing2Radius = THREE.MathUtils.lerp(2.0, 12.0, normX); 
      
      const invertedY = 1.0 - normY;
      mouseHighsTurbulence = Math.max(0.0, Math.pow(invertedY, 3) * 40.0); 
    }
  });

  addEventListener('keydown', (event) => {
    if (event.repeat) return;
    if (event.code === 'KeyP') setMode(mode === 'LAB' ? 'PERFORMANCE' : 'LAB');
    if (event.code === 'KeyR') simulation.reset();

    // Estos disparadores ahora funcionan igual en LAB y en PERFORMANCE.
    if (event.code === 'ShiftLeft' || event.code === 'ShiftRight') isShiftDown = true;
    if (event.code === 'KeyZ') isZDown = true;
    if (event.code === 'KeyX') isXDown = true;
    if (event.code === 'KeyC') isCDown = true;
    if (event.code === 'KeyV') isVDown = true;
    if (event.code === 'Space') {
      event.preventDefault();
      isSpaceDown = true;
    }
  });

  addEventListener('keyup', (event) => {
    if (event.code === 'ShiftLeft' || event.code === 'ShiftRight') isShiftDown = false;
    if (event.code === 'KeyZ') isZDown = false;
    if (event.code === 'KeyX') isXDown = false;
    if (event.code === 'KeyC') isCDown = false;
    if (event.code === 'KeyV') isVDown = false;
    if (event.code === 'Space') isSpaceDown = false;
  });

  addEventListener('resize', () => {
    camera.aspect = innerWidth / innerHeight;
    camera.updateProjectionMatrix();
    renderer.setSize(innerWidth, innerHeight);
    renderTarget.setSize(innerWidth, innerHeight); 
  });

  simulation.reset();

  renderer.setAnimationLoop(() => {
    if (!paused) {
      params.time.value += params.dt.value * params.timeScale.value;
      simulation.stepSimulation();
    }

    // ---- Progreso suave de los triggers de teclado (corre en ambos modos) ----
    const dtFrames = 1 / 60;
    if (isSpaceDown) kickProgress = Math.min(1.0, kickProgress + (dtFrames / 0.15));
    else kickProgress = Math.max(0.0, kickProgress - (dtFrames / 0.25));

    if (isCDown) colorProgress = Math.min(1.0, colorProgress + (dtFrames / 0.2));
    else colorProgress = Math.max(0.0, colorProgress - (dtFrames / 0.2));

    if (isVDown) vProgress = Math.min(1.0, vProgress + (dtFrames / 0.15));
    else vProgress = Math.max(0.0, vProgress - (dtFrames / 0.25));

    // ---- Combinamos baseState (sliders/presets) + efectos de teclado ----
    let curRingRadius = baseState.ringRadius;
    let curGrav = baseState.gravityStrength;
    let curGrav2 = baseState.ring2Gravity;
    let curRing2Radius = (mode === 'PERFORMANCE' && mouseRing2Radius !== null)
      ? mouseRing2Radius
      : baseState.ring2Radius;
    let curHighsTurbulence = (mode === 'PERFORMANCE' && mouseHighsTurbulence !== null)
      ? mouseHighsTurbulence
      : baseState.highsTurbulence;
    let curSwirl = baseState.swirlStrength;
    let curHighsSwirl = baseState.highsSwirl;
    let curFishEye = baseState.fishEye;
    let curAberration = baseState.chromaticAberration;
    let curBloom = baseState.bloomStrength;
    let curVignette = baseState.vignette;
    let curDamping = baseState.damping;
    let curTimeScale = 1.0;

    if (isShiftDown) {
      curDamping = 0.4;
      curTimeScale = 0.05;
    }
    if (isZDown) {
      curSwirl = -25.0;
      curHighsSwirl = -30.0;
    }
    if (isXDown) {
      curRingRadius = 0.1;
      curRing2Radius = 0.1;
      curGrav = 35.0;
      curGrav2 = 35.0;
      curFishEye = -1.2;
    }

    params.kickForce.value = THREE.MathUtils.lerp(0.0, 15.0, kickProgress);
    if (!isXDown) {
      curRingRadius = THREE.MathUtils.lerp(curRingRadius, 4.5, kickProgress);
      curFishEye = THREE.MathUtils.lerp(curFishEye, 2.5, kickProgress);
    }
    if (!isShiftDown) {
      curAberration = THREE.MathUtils.lerp(curAberration, 0.12, kickProgress);
    }
    
    curBloom = THREE.MathUtils.lerp(curBloom, 0.050, kickProgress);
    curVignette = THREE.MathUtils.lerp(curVignette, 2.0, kickProgress);

    params.ringRadius.value = curRingRadius;
    params.gravityStrength.value = curGrav;
    params.ring2Gravity.value = curGrav2;
    params.ring2Radius.value = curRing2Radius;
    params.swirlStrength.value = curSwirl;
    params.highsSwirl.value = curHighsSwirl;
    params.highsTurbulence.value = curHighsTurbulence;
    params.fishEye.value = curFishEye;
    params.chromaticAberration.value = curAberration;
    params.bloomStrength.value = curBloom;
    params.vignette.value = curVignette;
    params.damping.value = curDamping;
    params.timeScale.value = curTimeScale;
    params.colorPhase.value = THREE.MathUtils.lerp(0.0, 1.0, colorProgress);
    params.kaleidoscope.value = THREE.MathUtils.lerp(0.0, 1.0, vProgress);

    orbit.update();

    renderer.setRenderTarget(renderTarget);
    renderer.clear();
    renderer.render(scene, camera);

    renderer.setRenderTarget(null);
    renderer.clear();
    renderer.render(postScene, postCamera);
  });
}

main().catch((error) => {
  console.error(error);
  const pre = document.createElement('pre');
  pre.style.cssText = 'position:fixed;inset:16px;white-space:pre-wrap;color:#fff;z-index:50';
  pre.textContent = String(error?.stack || error);
  document.body.append(pre);
});
```

LAB PANEL
```
function rangeRow(parent, label, object, key, min, max, step, onInput, getValue) {
  const wrap = document.createElement('div');
  wrap.className = 'row';
  const lab = document.createElement('label');
  const name = document.createElement('span');
  const value = document.createElement('span');
  value.className = 'value';
  name.textContent = label;
  lab.append(name, value);
  const input = document.createElement('input');
  input.type = 'range';
  input.min = String(min);
  input.max = String(max);
  input.step = String(step);
  input.value = String(object[key]);
  const refresh = () => {
    object[key] = Number(input.value);
    value.textContent = Number(input.value).toFixed(step < 0.01 ? 3 : 2);
    onInput?.(object[key]);
  };
  input.addEventListener('input', refresh);
  refresh();
  wrap.append(lab, input);
  parent.append(wrap);
  return {
    input,
    refresh() {
      if (getValue) {
        const next = Number(getValue());
        object[key] = next;
        input.value = String(next);
        value.textContent = next.toFixed(step < 0.01 ? 3 : 2);
      }
    }
  };
}

function button(parent, label, onClick) {
  const b = document.createElement('button');
  b.textContent = label;
  b.addEventListener('click', onClick);
  parent.append(b);
  return b;
}

export function createLabPanel({ params, onReset, onPreset, onModeChange, onPauseChange }) {
  const refreshers = [];
  const panel = document.createElement('aside');
  panel.className = 'panel';
  
  panel.innerHTML = `
    <style>
      .desc { font-size: 10px; color: #8892b0; margin-top: -6px; margin-bottom: 12px; line-height: 1.3; }
    </style>
    <h1>U3 · LesAlpx Instrument</h1>
    <p>Post-Procesamiento Activo.</p>
  `;

  const state = {
    ringRadius: params.ringRadius.value,
    gravityStrength: params.gravityStrength.value,
    swirlStrength: params.swirlStrength.value,
    
    ring2Radius: params.ring2Radius.value,
    ring2Gravity: params.ring2Gravity.value,
    highsSwirl: params.highsSwirl.value,
    highsTurbulence: params.highsTurbulence.value,
    
    damping: params.damping.value,

    fishEye: params.fishEye.value,
    chromaticAberration: params.chromaticAberration.value,
    bloomStrength: params.bloomStrength.value,
    vignette: params.vignette.value
  };

  const gravesGroup = document.createElement('div');
  gravesGroup.className = 'group';
  gravesGroup.innerHTML = `
    <h2>1. Graves (Moradas)</h2>
    <p class="desc">Conforma la base rítmica. Espacio hace estallar este anillo (kick).</p>
  `;
  panel.append(gravesGroup);
  refreshers.push(rangeRow(gravesGroup, 'Radio Anillo', state, 'ringRadius', 0, 10, 0.1, (v) => params.ringRadius.value = v, () => params.ringRadius.value));
  refreshers.push(rangeRow(gravesGroup, 'Atracción a Base', state, 'gravityStrength', 0, 10, 0.1, (v) => params.gravityStrength.value = v, () => params.gravityStrength.value));
  refreshers.push(rangeRow(gravesGroup, 'Vel. Rotación', state, 'swirlStrength', -10, 10, 0.1, (v) => params.swirlStrength.value = v, () => params.swirlStrength.value));

  const agudosGroup = document.createElement('div');
  agudosGroup.className = 'group';
  agudosGroup.innerHTML = `
    <h2>2. Agudos (Azules)</h2>
    <p class="desc">En Performance, el Ratón controla su radio y turbulencia.</p>
  `;
  panel.append(agudosGroup);
  refreshers.push(rangeRow(agudosGroup, 'Radio Anillo 2', state, 'ring2Radius', 0, 15, 0.1, (v) => params.ring2Radius.value = v, () => params.ring2Radius.value));
  refreshers.push(rangeRow(agudosGroup, 'Atracción a Anillo 2', state, 'ring2Gravity', 0, 10, 0.1, (v) => params.ring2Gravity.value = v, () => params.ring2Gravity.value));
  refreshers.push(rangeRow(agudosGroup, 'Caos / Turbulencia', state, 'highsTurbulence', 0, 20, 0.1, (v) => params.highsTurbulence.value = v, () => params.highsTurbulence.value));

  const physicsGroup = document.createElement('div');
  physicsGroup.className = 'group';
  physicsGroup.innerHTML = `
    <h2>3. Globales</h2>
  `;
  panel.append(physicsGroup);
  refreshers.push(rangeRow(physicsGroup, 'Fricción (Damping)', state, 'damping', 0, 1, 0.01, (v) => params.damping.value = v, () => params.damping.value));

  const postGroup = document.createElement('div');
  postGroup.className = 'group';
  postGroup.innerHTML = `
    <h2>4. Lente (Post-Procesamiento)</h2>
    <p class="desc">Z: Reversa | X: Implosión | C: Muta Colores</p>
  `;
  panel.append(postGroup);
  refreshers.push(rangeRow(postGroup, 'Fish Eye', state, 'fishEye', -0.5, 1.0, 0.01, (v) => params.fishEye.value = v, () => params.fishEye.value));
  refreshers.push(rangeRow(postGroup, 'Aberración Crom.', state, 'chromaticAberration', 0, 0.05, 0.001, (v) => params.chromaticAberration.value = v, () => params.chromaticAberration.value));
  refreshers.push(rangeRow(postGroup, 'Bloom (Glow)', state, 'bloomStrength', 0, 0.02, 0.001, (v) => params.bloomStrength.value = v, () => params.bloomStrength.value));
  refreshers.push(rangeRow(postGroup, 'Viñeta', state, 'vignette', 0, 2.0, 0.05, (v) => params.vignette.value = v, () => params.vignette.value));

  const actions = document.createElement('div');
  actions.className = 'group';
  actions.innerHTML = '<h2>Acciones</h2>';
  panel.append(actions);
  button(actions, 'Reset', onReset);
  button(actions, 'LAB / PERFORMANCE', () => onModeChange());

  document.body.append(panel);

  return {
    element: panel,
    setVisible(visible) { panel.classList.toggle('hidden', !visible); },
    refresh() { for (const item of refreshers) item.refresh(); }
  };
}
```

### AUTOEVALUACIÓN

| Criterio | Peso | Qué debe demostrar la evidencia | Valoración (0-100) | Enlace / Evidencia |
| :--- | :---: | :--- | :---: | :--- |
| **Trazabilidad y comprensión del sistema** | 25 | Puedo señalar y explicar estado, fuerzas, integración, render y controles; además puedo ubicar qué partes produjo o modificó la IA. | 20 | [Enlace o descripción] |
| **Verificación del algoritmo de fuerzas** | 25 | Estudié en detalle el proyecto y aunque no comprenda toda la sintaxis, puedo identificar su arquitectura, sus partes, puedo aislar una fuerza central, formular una predicción, la ejecuté ya analicé, comparé el resultado, cambié deliberadamente un signo o parámetro y expliqué la diferencia. | 22 | [Enlace o descripción] |
| **Diseño de fuerzas e intención** | 20 | Las fuerzas y sus parámetros hacen perceptible una intención; el comportamiento surge de la dinámica y no de trayectorias previamente dibujadas. | 20 | [Enlace o descripción] |
| **Instrumento, score e interpretación** | 15 | El score conecta la escucha con decisiones; escogí pocos controles expresivos y puedo conducir el sistema en vivo sin que el audio lo controle automáticamente. | 15 | [Enlace o descripción] |
| **Experimentación y criterio frente a la IA** | 10 | Comparé alternativas, registré hallazgos y descartes, corregí propuestas de IA y puedo justificar por qué conservé la versión presentada. | 10 | [Enlace o descripción] |
| **Entrega técnica y documentación** | 5 | La URL pública abre; la bitácora permite verificar el proceso. | 5 | [URL](https://valencia33.github.io/UNIDAD3-SIMULACION/) |
| **Total Puntos** | **100** | *Suma total de tu autoevaluación* | **[ 92/100 ]** | |

NOTA: 4.6
