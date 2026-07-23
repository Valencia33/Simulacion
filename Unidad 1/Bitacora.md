# UNIDAD 1: ALETORIEDAD
## Actividad 1

Despues de observar los videos y leer los ensayos de Tyler Hobbs comprendo que el concepto de *Aletoriedad* en el arte es para que el producto final sea distinto cada vez que se iter.

## Actividad 2

```py
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let walker;

function setup() {
  createCanvas(1000, 1000);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
    this.hue = 0
    this.r = 1;
  }

  show() {
    stroke(this.hue, this.hue + this.hue, this.hue * 3);
    circle(this.x,this.y,this.r)
  }

  step() {
    const choice = floor(random(4));
    
    this.hue++;
    if(this.hue == 255)
    {
      this.hue = 0;
    }

    this.r++;
    if(this.r == 25)
    {
      this.r = 0;
    }
    
    if (choice == 0) {
      this.x+=10;
    } else if (choice == 1) {
      this.x-=10;
    } else if (choice == 2) {
      this.y+=10;
    } else {
      this.y-=10;
    }
  }
}
```

<img width="700" height="700" alt="image" src="https://github.com/user-attachments/assets/5d20de4f-e826-43d3-b624-f4715433e39e" />

Al analizar el código entendí rapidamente donde debía de realizar cambios para lograr el resultado que esperaba, en un principio sabía que quería que se viera como una serpiente dando vueltas, no sería posible hacerlo en realidad a menos de que guardará los datos de cada circulo y los actualizara frame a frame entonces opté por una solución más simple que fue no hacerlo y usar un contador que iba de 0 a 25, aumentar el "salto" que se daba entre circulos y tambien cambiar el color.

## Actividad 3

1.) **En tus propias palabras cuál es la diferencia entre una distribución uniforme y una no uniforme de números aleatorios.**

Una distribución uniforme tiene la misma probabilidad de generar todos los números en un rango. Una distribución no uniforme tiene mayor probabilidad en algunos valores, en el caso de la distribución gaussiana, este tiene mayor probabilidad de generar los valores que están cerca de la media.

2.) **Modificar el código para que tenga mayor probabilidad de moverse a la derecha.**

Lo que hice fue utilizar randomGaussian() para que la probabilidad de generar valores cercanos a 0 sea mayor

```py
let choice = floor(randomGaussian(0,3));
    if(choice < 0)
    {
      choice = 0;
    }
```
<img width="700" height="700" alt="image" src="https://github.com/user-attachments/assets/ebb46080-b11f-4ef9-b143-7e65e1f01755" />

3.) **otras cosas**

Hice que tuviera un wrap para que el patrón no se escapara

```py
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

let walker;

function setup() {
  createCanvas(700, 700);
  walker = new Walker();
  background(255);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
    this.hue = 0
    this.r = 1;
  }

  show() {
    stroke(this.hue, this.hue + this.hue, this.hue * 3);
    circle(this.x,this.y,this.r)
  }

  step() {
    let choice = floor(randomGaussian(0,3));
    if(choice < 0)
    {
      choice = 0;
    }
    
    this.hue++;
    if(this.hue == 255)
    {
      this.hue = 0;
    }

    this.r++;
    if(this.r == 25)
    {
      this.r = 0;
    }
    
    if (choice == 0) {
      this.x+=10;
    } else if (choice == 1) {
      this.x-=10;
    } else if (choice == 2) {
      this.y+=10;
    } else {
      this.y-=10;
    }

    if(this.x > width) this.x =0;
    if(this.y > height) this.y = 0;
    if (this.x < 0) this.x = width;
    if(this.y < 0) this.y = height;
  }
}

```
## Actividad 4

1.) **Crea un nuevo sketch en p5.js que represente una distribución normal, pero visualizándola de manera diferente a la del ejemplo.**

El código del ejercicio:

```py
// The Nature of Code
// Daniel Shiffman
// http://natureofcode.com

function setup() {
  createCanvas(640, 240);
  background(255);
}

function draw() {
  // A normal distribution with mean 320 and standard deviation 60
  let x = randomGaussian(320, 60);
  noStroke();
  fill(0, 10);
  circle(x, 120, 16);
}
```

Este código es bastante simple, utiliza el número que le devuelve la distribución gaussiana para mover un circulo bastante tenue en x.

Para la modificación que le quiero hacer voy a hacer lo mismo, pero cambiando el tamaño de tal forma que en width/2 sea lo más grande y a medida que va a los extremos se vuelva más pequeño. No solo eso si no que tambien voy a modificar el color, para que verde sea cuando está en el centro y rojo en los extremos e interpole entre esos.

<img width="600" height="600" alt="image" src="https://github.com/user-attachments/assets/253d4232-3bd0-430f-b22e-3fbbd3ebec89" />

Lo logré, lo hice todo sin ayuda de la IA excepto el segundo lerpColor donde usando el método del profe de discutir con la IA me di cuenta que era solamente que tenia c1 y c2 trucados. No solo eso pero me dio una solución mejor al tema del color y era calcularlo con distancia en vez de con rangos, que me pareció una excelente idea pero al final no la implementé

```py
function setup() {
  createCanvas(600, 600);
  background(255);
}

function draw() {
  let c1 = color(0,255,0,40);
  let c2 = color(255,0,0,40);
  let x = randomGaussian(300, 100);
  
  let size = x;

  if(size > 300)
  {
    size = 300 - (x-300);
    finalColor =  lerpColor(c2,c1,1 + (size-300)/(300));
  }
  else
  {
    finalColor = lerpColor(c2,c1,(size)/(300));
  }
  
  noStroke();
  fill(finalColor);
  circle(x, 300, size);
}

```
## Actividad 5

Si utilizamos partes del código presentado por Daniel Shiffman podemos lograr simular un levy flight, sin embargo no lo es del todo pues según tengo entendido la probabilidad de cualquier longitud de salto EXISTE, pero disminuye a medida que el tamaño de salto aumenta. Dicho esto, en un principio hice exactamente eso:

```py
let walker;

function setup() {
  createCanvas(700, 700);
  walker = new Walker();
  background(0);
}

function draw() {
  walker.step();
  walker.show();
}

class Walker {
  constructor() {
    this.x = width / 2;
    this.y = height / 2;
    this.hue = 0
    this.r = 1;
  }

  show() {
    stroke(this.hue, this.hue + this.hue, this.hue * 3);
    fill(0)
    circle(this.x,this.y,this.r)
  }

  step() {
    
    let choice = floor(random(4));

    //cambio color
    this.hue++;
    if(this.hue == 255)
    {
      this.hue = 0;
    }

    //cambio radio
    this.r++;
    if(this.r == 25)
    {
      this.r = 0;
    }

    //implementación levy flight
    let r = random(1);
    if (r < 0.02)
    {
      let step = 300;
    let stepx = random(-step, step);
    let stepy = random(-step, step);
    this.x += stepx;
    this.y += stepy;
    }
    

    //pasos "normales"
    if (choice == 0) {
      this.x+=10;
    } else if (choice == 1) {
      this.x-=10;
    } else if (choice == 2) {
      this.y+=10;
    } else {
      this.y-=10;
    }

    if(this.x > width) this.x =0;
    if(this.y > height) this.y = 0;
    if (this.x < 0) this.x = width;
    if(this.y < 0) this.y = height;
  }
}
```
<img width="1200" height="1200" alt="image" src="https://github.com/user-attachments/assets/2dfec277-0e4e-4633-b8c1-aad1d9c997a9" />

Ahora bien, ese código simula bastante bien como se vería un Levy flight real, pero para hacerlo REAL debemos quitar la linea de let random(1) y el if, y en vez utilizar el random para calcular la distancia del salto, de esta forma la probabilidad está directamente relacionada con la distancia del salto.

entonces mejor se calcula el movimiento así:

```py
  let step = 5/(random(1)**2)
    let stepx = random(-step, step);
    let stepy = random(-step, step);
    this.x += stepx;
    this.y += stepy;
```

<img width="1200" height="1200" alt="image" src="https://github.com/user-attachments/assets/fe2c5a64-d415-488b-b6b7-12f1d200ace8" />

## Actividad 6

Listo, la verdad es que no se me ocurrieron muchas más formas de visualizarlo más allá de lo que proponía el ejercicio, ENTONCES decidí hacer lo mismo pero más estilizado. En la esquina de arriba a la derecha se presentan dos valores; 1.) el valor que devuelve noise(t) y 2.) la diferencia de noise(t) en fn y fn+1, esto debido a que en esta visualización el color juega un papel crucial, y es que entre más rojo sea el color significa que el cambio entre valores fue más brusco.

```py
let t = 0
let perlinValue
let diference
let frameValue = 0
let c1
let c2
let diff
let x = 500

function setup() {
  createCanvas(1000, 1000);

  c1 = color(0,255,0)
  c2 = color(255,0,0)
}

function draw() {
  background(220,15);
  
  perlinValue = noise(t) // genera valor
  diference = frameValue-perlinValue
  if(abs(diference*100) > 1)
  {
    diff = 1
  }  
  else
  {
    diff = abs(diference*100)
  }
  fill(lerpColor(c1,c2,diff)) //calcula color dependiendo del cambio
  noStroke()
  frameValue = perlinValue // guarda pal siguiente frame
  
  circle(x,perlinValue*1000,50) //dibuja el circulo

  //====== INCREMENTO VARIABLES=========
  t += 0.01
  x+=5

  if(x>width) x = 0

  //=====TEXTO============
  fill(150)
  square(30,30,200)
  textSize(50)
  fill(lerpColor(c1,c2,diff))
  text(round(perlinValue,2),50,90)
  fill(0)
  text(round(diff,3),50,190)
  
}
```

<img width="1000" height="1000" alt="image" src="https://github.com/user-attachments/assets/0c2a4856-5cc6-4012-a1d7-07a57cca5318" />


<img width="1000" height="1000" alt="image" src="https://github.com/user-attachments/assets/e39c2d11-bf50-438a-8e6b-00d60e8820ab" />

ahí si observa que entre mayor la diferencia entre frames entonces más rojo será el color.

## Actividad 7

**El sistema deberá interpretar los siguientes momentos:**

 - Posibilidad: todas las direcciones parecen posibles.
 - Tendencia: una pequeña preferencia repetida termina construyendo una dirección.
 - Normalidad: la mayoría de los recorridos permanece cerca de lo habitual.
 - Excepción: un evento improbable permite descubrir un territorio nuevo.
 - Influencia: la presencia del visitante transforma lo que puede ocurrir.
   
No debes ilustrar literalmente las frases. Debes traducirlas en comportamientos, trayectorias, ritmos, concentraciones o transformaciones.

**Condiciones de diseño**

  - La experiencia debe ser una sola pieza coherente, no cinco sketches separados.
  - Debe combinar significativamente al menos tres conceptos de la unidad: caminata aleatoria, distribuciones de probabilidad, distribución normal, Lévy flight o ruido Perlin.
  - La interacción debe modificar las probabilidades o reglas del sistema. No basta con cambiar colores, avanzar escenas o dibujar directamente.
  - El sistema debe continuar funcionando cuando nadie interactúa.
  - Cada ejecución debe producir variaciones sin perder su identidad visual.
  - Formato 9:16, full screen y ejecución interactiva en tiempo real.

### Reto de diseño
<a name="e1"></a>
**CONCEPTO**

Ultimamente, me preocupa mucho la dirección que tome la humanidad con respecto al medio ambiente, me parece que por muchos años hemos crecido sin preguntarnos como nuestros hábitos de consumo afectan el medio ambiente. La naturaleza, como un todo, es algo infinitamente complejo, con infinidad de variables, que sin la presencia de humanos se transforma y crece a partir de reglas impuestas desde un principio. Sin embargo, la presencia de la humanidad, ha desviado los procesos usuales de la naturaleza y la ha afectado de tal manera que volver a la normalidad tomará una escala de tiempo inconcebible para nosotros.

Es por eso, que en mi experiencia pretendo darle importancia a ese concepto: Como la intervención humana afecta de forma indefinida un ecosistema.

 - Posibilidad: El ecosistema CRECE de cualquier forma, depende de tantas variables que es casi imposible que salga igual 2 veces, REPRESENTA la forma en como la naturaleza evoluciona.
 - Tendencia: LOS CORALES, es mucho más probable que crezan hacía arriba, intentado alcanzar el agua que es lo que les da vida
 - Normalidad: LA INTERACCIÓN ENTRE AGUA Y TIERRA, se repelen y terminan creando una especie de armonia donde ignorar hace que creen un lugar con sentido
 - Excepción: El comportamiento de la vida trata de imitar lo efimero que es, de tal forma que aparece y desaparece de todos lo lugares del canva, dejando una huella pequeña en un espacio más vasto
 - Influencia: Como en la vida real, la presencia del ser humano hace que el ecosistema pierda el equilibrio, muera, sea afectado profundamente, tan profundamente que se demora mucho tiempo en recuperarse

1.) Posibilidad

Para este momento, desde su descripción se me ocurre que lo más obvio sería utilizar la distribución NO UNIFORME, me hace sentir que como todos los caminos son posibles entonces todo puede pasar. No solo eso pero tambien me gustaría la opción de que el usuario pueda borrar el tablero, entonces antes de empezar, eso es lo primero que haré.

Me tomó más de lo que me gustaría admitir, pq lo estaba haciendo en un método aparte y la lógica estaba detrás de un while, por lo que no dibujaba en la pantalla si no que lo hacia INSTANTANEo, entonces puse un if en draw().
```py
//=== BORRAR PANTALLA ===
  if (eraseScreen && radii < width + 500) {
    fill(0);
    noStroke();
    circle(width/2, height/2, radii);
    
    radii += 50;
  }
```
Lo mejoré un poquitin para que fuera más claro que borra, encima no solo eso pero tambien se me olvidó que tenía que reiniciar las variables para volver a borrar

```py
if (eraseScreen) {
    fill(255);
    noStroke();
    circle(width/2, height/2, radii+15);
    fill(0)
    circle(width/2, height/2, radii);
    radii += 100;

    if (radii > width + 500) {
      eraseScreen = false;
    }
  }
}

function keyPressed() {
  if (key === 'e') {
    radii = 0;
    eraseScreen = true;
  }
}
```
BUENO AHORA Sí, la parte de POSIBILIDAD y la verdad del resto de propuestas, como estoy partiendo de los ejercicios que salieron de la parte del walker entonces realmente no hay mucho que decir aparte de las cosas que ya implemneté en ejercicios pasados, entonces voy a colocar acá los códigos y mencionó cualauqier cambio que haya hecho.

en un principio, cada uno de los comportamientos decidí meterlos a métodos de cada uno y controlarlos como si fuera una maquina de estados que maneja el usuario.

```py
 tendencia(){
    //pasos "normales" - TENDENCIA
    let choice = floor(random(8));

    if (choice == 0) {
      this.x+=15;
    } else if (choice == 1) {
      this.x-=15;
    } else if (choice == 2) {
      this.y+=15;
    } else {
      this.y-=15;
    }
  }
  
  normalidad(){
    let perlinValue = noise(this.t)

    //====== INCREMENTO VARIABLES=========
    this.t += 0.01
    this.x+=5
    this.y = perlinValue*1000
  }
  
  posibilidad(){
    //pasos "normales" - POSIBILIDAD
    let choice = floor(random(4));

    if (choice == 0) {
      this.x+=15;
    } else if (choice == 1) {
      this.x-=15;
    } else if (choice == 2) {
      this.y+=15;
    } else {
      this.y-=15;
    }
  }

  excepcion(){
     //implementación levy flight - EXCEPCIÓN
    let r = random(1);
    if (r < 0.02)
    {
      let step = 300;
    let stepx = random(-step, step);
    let stepy = random(-step, step);
    this.x += stepx;
    this.y += stepy;
    }
  }
```
esta es la primera versión, aún está muy sujeta a cambios puesto que literalmente pegué e hice cambios muy pequeños para adaptarlo, pero en si es lo mimso que ya hicimos, con la excepción de que TENDENCIA es el mimso de posibilidad pero se crean números random mayores a 4 por lo que y -= 15 es mucho más probable de suceder.

Dos complicaciones en esta etapa de diseño; Una forma de que el usuario sepa que controles hay/como puede influir y un concepto. La primera complicación es mucho más simple de resolver que la otra, mi solución fue un 

Ahora lo que sigue es añadir un par de interacciones para el usuario.

ok hubo un par de cambios precisamente por eso de que quería meter más interacciones pal usuairo, una de sas fue que pudiera colocar más walkers, el tema es que eso hizo que tuviera que cambiar de un solo objeto a un array y que cada que llamara sus coasa en draw() fuera con un for

```py
function mousePressed() {
  let nuevoWalker = new Walker();
  nuevoWalker.x = mouseX;
  nuevoWalker.y = mouseY;
  
  if (walkers.length > 0) {
    nuevoWalker.modo = walkers[0].modo;
  }
  
  walkers.push(nuevoWalker);
}
```
esto es para cambiar de modos.
```py
function keyPressed() {
  if (key === 'e') {
    radii = 0;
    eraseScreen = true;
  }
  else if(keyCode === 39) {
    for (let w of walkers) {
      w.modo++;
      if (w.modo > 4) w.modo = 1;
    }
  }
  else if(keyCode === 37) {
    for (let w of walkers) {
      w.modo--;
      if (w.modo < 1) w.modo = 4;
    }
  }
}
```
y ahora este es mi método step()
```
step() {
    if (this.modo === 1) this.posibilidad();
    else if (this.modo === 2) this.tendencia();
    else if (this.modo === 3) this.normalidad();
    else if (this.modo === 4) this.excepcion();

    if(this.x > width) this.x = 0;
    if(this.y > height) this.y = 0;
    if(this.x < 0) this.x = width;
    if(this.y < 0) this.y = height;
  }
```
He hecho vairas cosas, la posibilidad de añadir mas bichitos me ha dado más problemas, pues quise hacer que al crear uno nuevo este tuviera un color distinto, entonces añadí esa interacción. Al final mi solución fue pasarle el tipo de color con el que se crea y mantener un contador por lo que haora mi metodo cuando se presiona el mouse se ve así: 

```
function mousePressed() {
  let nuevoWalker = new Walker(turnoColor);
  nuevoWalker.x = mouseX;
  nuevoWalker.y = mouseY;
  
  walkers.push(nuevoWalker);
  
  turnoColor++;
  if (turnoColor > 3) {
    turnoColor = 0;
  }
}
```
Con eso ya tengo lo principal de la appplicacion, pero falta LO MÁS DIFICIL 
que es la interacción del usuario, para esto planeaba hacer algo con la posición del mouse, ah buneo eso y que se me olvidó que la resolución en realidad es vertical.

Quiero hacer como una especie de atractor, que aprovechando que estoy haciendo eso con objetos debería ser bastante facil si lo hago en el step(), para eso entonces, como igual quiero que sigan siendo aleatorios los movimientos entonces voy a hacer que el mouse afecte los cocsitos que están a determinado radio de el, en pseudo codigo sería algo como

sacar distancia de cosito a mouse
chequear si la distnacia es menor que x
si si lo es entonces 
x lerp a la posición del mouse
y lerp a la posición del mouse

```
let distanciaMouse = dist(this.x, this.y, mouseX, mouseY);
    
    if (distanciaMouse < 300) {
        this.x += (mouseX - this.x) * 0.15; 
        this.y += (mouseY - this.y) * 0.15;
      }
```
Tengo una complicacion, la primera es que el usuario aún no sabe que controles tiene la experiencia por lo que vamos a solucionar eso. La solución al primer problema es bastante simple, un cuadrado con las instrucciones, y como estorba, bajarle la opacidad graudalmente 

```py

  //== INSTRUCCIONES ==
  fill(255,opacity)
  noStroke()
  rect(20,20,280,110,20)
  fill(0,opacity)
  textSize(20)
  text("+ click - crear walker" , 40,50)
  text("+ flechitas - cambiar modo" , 40,80)
  text("+ E - borrar" , 40,110)
  opacity -= 1
  if(opacity < 0) opacity = 0
```
no es tan simple. por alguna razón que desconozco mi lógica no funciona. Es muy charro pq se supone que fill(gray,alpha) entonces si disminuyo opacity hasta que sea 0 se debería dejar de ver, cosa que no pasa por alguna razón, sin embargo si cambio los valores alcanzo un resultado similar, por lo que voy a optar por dibujar las instrucciones despues del walker para que de esa forma pareza que logra el mismo resultado, y no haya un cuadrado negro ahí de la nada. 

Lo logré de una forma más elegante, utilicé un IF que encierra el bloque anterior, por lo que de esa forma, en el siguiente frame en el que opacity ya sea 0, no va a correr y va a dibujar encima del cuadrado negro.

#### DESARROLLO CONCEPTO

Hasta ahora he tenido en cuenta una forma muy básica de mi concepto. El punto actual del proyecto es centrarse más que todo en COMO CRECE LA NATURALEZA, más sin embargo está creciendo independiente de SI MISMA y la interacción humana afecta MÁS NO DESTRUYE y no vuelve a su orden, este es el estado actual del proyecto:

<img width="1080" height="1920" alt="image" src="https://github.com/user-attachments/assets/431b76a8-45c6-496d-aadc-51f0b757595d" />

```js
let walkers = [];
let radii = 0;
let eraseScreen = false;
let turnoColor = 0;
let opacity = 255;

function setup() {
  createCanvas(1080, 1920);
  walkers.push(new Walker(turnoColor));
  turnoColor++;
  background(0);
}

function draw() {

  //====== WALKER ======
  for (let i = 0; i < walkers.length; i++) {
    walkers[i].step();
    walkers[i].show();
  }

  //== INSTRUCCIONES ==
  if(opacity != 0)
  {
   fill(opacity)
  noStroke()
  rect(20,20,280,110,20)
  fill(0)
  textSize(20)
  text("+ click - crear walker" , 40,50)
  text("+ flechitas - cambiar modo" , 40,80)
  text("+ E - borrar" , 40,110)
  opacity -= 1
  if(opacity < 0) opacity = 0 
  }

  //=== BORRAR PANTALLA ===
  if (eraseScreen) {
    fill(255);
    noStroke();
    circle(width/2, height/2, radii+15);
    fill(0);
    circle(width/2, height/2, radii);
    radii += 100;

    if (radii > width + 1500) {
      eraseScreen = false;
    }
  }
}

class Walker {
  constructor(tipoColor) {
    this.x = random(width);
    this.y = random(height);
    this.hue = 0; 
    this.tipoColor = tipoColor; 
    this.r = random(25);
    this.t = random(10000);
    this.modo = floor(random(1, 5));
  }

  show() {

    strokeWeight(15)
      
    if (this.tipoColor === 0) {
      stroke(this.hue, this.hue + this.hue, this.hue * 3); 
    } else if (this.tipoColor === 1) {
      stroke(this.hue * 3, this.hue + this.hue, this.hue); 
    } else if (this.tipoColor === 2) {
      stroke(this.hue, this.hue * 3, this.hue + this.hue); 
    } else if (this.tipoColor === 3) {
      stroke(this.hue * 3, this.hue, this.hue+this.hue); 
    }

    fill(0);
    circle(this.x, this.y, this.r);
    
    //cambio color
    this.hue++;
    if(this.hue >= 85) {
      this.hue = 0;
    }

    //cambio radio
    this.r++;
    if(this.r >= 25) {
      this.r = 0;
    }
  }

  step() {
    if (this.modo === 1) this.posibilidad();
    else if (this.modo === 2) this.tendencia();
    else if (this.modo === 3) this.normalidad();
    else if (this.modo === 4) this.excepcion();

    /*
    let distanciaMouse = dist(this.x, this.y, mouseX, mouseY);
    
    if (distanciaMouse < 300) {
        this.x += (mouseX - this.x) * 0.15; 
        this.y += (mouseY - this.y) * 0.15;
      }
    */

    if(this.x > width) this.x = 0;
    if(this.y > height) this.y = 0;
    if(this.x < 0) this.x = width;
    if(this.y < 0) this.y = height;
  }

  tendencia() {
    //pasos "normales" - POSIBILIDAD
    let choice = floor(random(8));

    if (choice == 0) {
      this.x+=15;
    } else if (choice == 1) {
      this.x-=15;
    } else if (choice == 2) {
      this.y+=15;
    } else {
      this.y-=15;
    }
  }
  
  normalidad() {
    let perlinValue = noise(this.t);

    //====== INCREMENTO VARIABLES=========
    this.t += 0.01;
    this.x += 15;
    this.y = perlinValue * 1500;
  }
  
  posibilidad() {
    //pasos "normales" - POSIBILIDAD
    let choice = floor(random(4));

    if (choice == 0) {
      this.x+=15;
    } else if (choice == 1) {
      this.x-=15;
    } else if (choice == 2) {
      this.y+=15;
    } else {
      this.y-=15;
    }
  }

  excepcion() {
    //implementación levy flight - EXCEPCIÓN
    let r = random(1);
    if (r < 0.02) {
      let step = 300;
      let stepx = random(-step, step);
      let stepy = random(-step, step);
      this.x += stepx;
      this.y += stepy;
    } else {
      this.x += random(-10, 10);
      this.y += random(-10, 10);
    }
  }
}

function keyPressed() {
  if (key === 'e') {
    radii = 0;
    eraseScreen = true;
    walkers = [];
  }
  else if(keyCode === 39) {
    for (let w of walkers) {
      w.modo++;
      if (w.modo > 4) w.modo = 1;
    }
  }
  else if(keyCode === 37) {
    for (let w of walkers) {
      w.modo--;
      if (w.modo < 1) w.modo = 4;
    }
  }
}

function mousePressed() {
  let nuevoWalker = new Walker(turnoColor);
  nuevoWalker.x = mouseX;
  nuevoWalker.y = mouseY;
  
  walkers.push(nuevoWalker);
  
  turnoColor++;
  if (turnoColor > 3) {
    turnoColor = 0;
  }
}
```
Es por eso, que a partir de ahora, tomaré una lista de ideas para implementar QUE ADEMÁS COMPLEMENTEN el concepto:

1.) Los walker se afectan entre ellos, como si fueran planetas.
2.) La interacción del usuario CAMBIA PROBABILIDADES de los walker que no estén en el radio de acción Y ADEMÁS cambia de color los walker a un GRIS.
3.) Una vez el usuario interactua, un bloque negro crece en opacidad lentamente para dar a entender que el efecto humano se borra con el tiempo.
4.) Que la experiencia comience con una exploción.
5.) Que cada uno de los colores esté asociado a un comportamiento y una parte de la naturaleza: Azul (agua, ruido perlin), Verde (Plantas, distribución no uniforme), Rojo (Corales, Distribución gaussiana (que crezcan hacía arriba y  tengan la habilidad de multiplicarse)), Amarillo (Vida, Levy Flight). La interacción del humano, me gustaría que hiciera las cosas grises.
6.) Las relaciones entre los walker DEPENDE DE SUS TIPOS. CORALES Y AGUA SE ATRAEN, AGUA Y PLANTAS SE REPELEN, PLANTAS Y VIDA SE ATRAEN Y SE REPELEN.

1.) Los walker se afectan entre ellos, como si fueran planetas.

Lo primero que hice para esto fue hacer un repaso entero del código a ver que necesitaba cambios, en un principio la función mousePressed() reiniciaba modo en 0, ahora lo hace en 1 para que no entre al modo muerte por azar. Tambien eliminé la opción de cambiar de modo con las flechitas, pues ya no era necesario. Y AHORA LO QUE SIGUE ES DISEÑAR LA INTERACCIÓN ENTRE WALKERS. Para eso, crearé un nuevo método donde se calcula distancia y dependiendo del modo y la distancia actua de una manera.

en un principio, es bastante fácil, solo hay que encontrar la distancia entre un walker y los demás, para eso utilizo un for y la función dist().

```js
 for (let otro of otros) {
      if (otro !== this) {
        let d = dist(this.x, this.y, otro.x, otro.y);
```

una vez tengo la distancia tengo que hacer el SUPER IF para saber si es afectada o NO.

EN ESTA PARTE USÉ IA, necesitaba una forma de aplicar una fuerza progresiva y no sabía como, la solución de la IA FUE LA SIGUIENTE

```js
if (d > 0 && d < radioPercepcion) {
          let dx = otro.x - this.x;
          let dy = otro.y - this.y;

          if ((this.modo === 2 && otro.modo === 3) || (this.modo === 3 && otro.modo === 2)) {
            this.x += dx * fuerza;
            this.y += dy * fuerza;
          }
          else if ((this.modo === 3 && otro.modo === 1) || (this.modo === 1 && otro.modo === 3)) {
            this.x -= dx * fuerza;
            this.y -= dy * fuerza;
          }
          else if (this.modo === 1 && otro.modo === 4) {
            this.x += dx * fuerza;
          }
          else if (this.modo === 4 && otro.modo === 1) {
            this.x -= dx * fuerza;
          }
        }
```
De esta forma ya los walker se afectan entre si. LA INTERACCIÓN ES MUY SIMPLE, entonces está sujeta a cambios, pero por ahora mi segundo punto.

2.) La interacción del usuario CAMBIA PROBABILIDADES de los walker que no estén en el radio de acción Y ADEMÁS cambia de color los walker a un GRIS.

Este es bastante simple, es añadir otro estado para los walker, que se active SI ESTÁN DENTRO DEL RADIO DE ACCIÓN DEL MOUSE. entonces en el metodo step lo primero sería lo mismo, calcular la distancia y poner un if, despues poner que mode = 0 y en la parte donde se define su comportamiento por su modo añadir el método.

```js
let distanciaMouse = dist(this.x, this.y, mouseX, mouseY);
    
    if (distanciaMouse < 150 && (movedX !== 0 || movedY !== 0)) {
      if (this.modo !== 0) {
        this.modoOriginal = this.modo;
        this.modo = 0;
      }
      this.tiempoCorrupcion = millis(); 
    }
```
Método muerte

```js
 muerte()
  {

    this.x += random(-5, 5);
    this.y += random(-5, 5);

    if (millis() - this.tiempoCorrupcion > this.tiempoRecuperacion) {
      this.modo = this.modoOriginal;
      this.r = 5; 
    }
  }
```

Cuando el mouse interactua con alguno en ese radio entonces se muere y revive despues de un rato.

buscnado he perdido mucho tiempo tratando de solucionar un problema y ya encontré algo interesante que no sabía que existia en p5js. Hay una función llamada createGraphics, que permite dibujar en un buffer distinto al que hemos estado utilizando hasta el momento. la solución que proponen es crear una especia de CAPA NUEVA con las misma resolución y dibujar en ella todo lo que necesito. ESTE ES UN CAMBIO GRANDE. entonces voy a guardar mi código acá, antes de hacer un daño.

```js
let walkers = [];
let radii = 0;
let eraseScreen = false;
let modo = 1;
let opacity = 255;

function setup() {
  createCanvas(1080, 1920);
  walkers.push(new Walker(modo));
  modo++;
  background(0);

  for(let i = 0; i < 20; i++){
    walkers.push(new Walker(floor(random(1, 5))));
  }
}

function draw() {

  //====== WALKER ======
  for (let i = 0; i < walkers.length; i++) {
    walkers[i].interactuar(walkers);
    walkers[i].step();
    walkers[i].show();
  }

  //== INSTRUCCIONES ==
  if(opacity != 0)
  {
   fill(opacity)
  noStroke()
  rect(20,20,250,80,20)
  fill(0)
  textSize(20)
  text("+ click - crear walker" , 40,50)
  text("+ E - borrar" , 40,80)
  opacity -= 1
  if(opacity < 0) opacity = 0 
  }

  //=== BORRAR PANTALLA ===
  if (eraseScreen) {
    fill(255);
    noStroke();
    circle(width/2, height/2, radii+15);
    fill(0);
    circle(width/2, height/2, radii);
    radii += 100;

    if (radii > width + 1500) {
      eraseScreen = false;
    }
  }

  //=== COSITO PAL MOUSE ===
  fill(0)
  strokeWeight(1)
  stroke(255)
  circle(mouseX,mouseY,150)

}

class Walker {
  constructor(modo) {
    this.x = random(width);

    this.modo = modo;
    this.modoOriginal = modo;
    this.tiempoCorrupcion = 0;
    this.tiempoRecuperacion = random(5000, 10000);
    
    if (this.modo === 2) {
      this.y = random(1000,height); 
    } else {
      this.y = random(height);
    }
    
    this.hue = 0; 
    this.r = random(25);
    this.t = random(10000);
  }

  show() {

    strokeWeight(15)
      
    if (this.modo === 2) {
      stroke(this.hue, this.hue + this.hue, this.hue * 3); //azul - agua
    } else if (this.modo === 4) {
      stroke(this.hue * 3, this.hue + this.hue, this.hue); //amarillo - vida
    } else if (this.modo === 1) {
      stroke(this.hue, this.hue * 3, this.hue + this.hue); //verde - plantas
    } else if (this.modo === 3) {
      stroke(this.hue * 3, this.hue, this.hue+this.hue); //rojo - corales
    } else if (this.modo === 0){
      stroke(this.hue, this.hue,this.hue); // GRIS MUERTE
    }

    fill(0);
    circle(this.x, this.y, this.r);
    
    //cambio color
    this.hue++;
    if(this.hue >= 85) {
      this.hue = 50;
    }

    //cambio radio
    this.r++;
    if(this.r >= 25) {
      this.r = 0;
    }
  }

  step() {

    let distanciaMouse = dist(this.x, this.y, mouseX, mouseY);
    
    if (distanciaMouse < 150 && (movedX !== 0 || movedY !== 0)) {
      if (this.modo !== 0) {
        this.modoOriginal = this.modo;
        this.modo = 0;
      }
      this.tiempoCorrupcion = millis(); 
    }
    
    if (this.modo === 1) this.posibilidad(); //verde
    else if (this.modo === 3) this.tendencia(); //corales
    else if (this.modo === 2) this.normalidad(); //azul
    else if (this.modo === 4) this.excepcion(); //vida
    else if (this.modo === 0) this.muerte();

    /*
    let distanciaMouse = dist(this.x, this.y, mouseX, mouseY);
    
    if (distanciaMouse < 300) {
        this.x += (mouseX - this.x) * 0.15; 
        this.y += (mouseY - this.y) * 0.15;
      }
    */

    if(this.x > width) this.x = 0;
    if(this.y > height) this.y = 0;
    if(this.x < 0) this.x = width;
    if(this.y < 0) this.y = height;
  }

  interactuar(otros) {
    let radioPercepcion = 500;
    let fuerza = 0.01;

    for (let otro of otros) {
      if (otro !== this) {
        let d = dist(this.x, this.y, otro.x, otro.y);

        if (d > 0 && d < radioPercepcion) {
          let dx = otro.x - this.x;
          let dy = otro.y - this.y;

          if ((this.modo === 2 && otro.modo === 3) || (this.modo === 3 && otro.modo === 2)) {
            this.x += dx * fuerza;
            this.y += dy * fuerza;
          }
          else if ((this.modo === 3 && otro.modo === 1) || (this.modo === 1 && otro.modo === 3)) {
            this.x -= dx * fuerza;
            this.y -= dy * fuerza;
          }
          else if (this.modo === 1 && otro.modo === 4) {
            this.x += dx * fuerza;
            this.y += dy * fuerza
          }
          else if (this.modo === 4 && otro.modo === 1) {
            this.x -= dx * fuerza;
            this.y -= dy * fuerza
          }
        }
      }
    }
  }

  tendencia() {
    //pasos "normales" - POSIBILIDAD
    let choice = floor(random(8));

    if (choice == 0) {
      this.x+=15;
    } else if (choice == 1) {
      this.x-=15;
    } else if (choice == 2) {
      this.y+=15;
    } else {
      this.y-=15;
    }
  }
  
  normalidad() {
    let perlinValue = noise(this.t);

    //====== INCREMENTO VARIABLES=========
    this.t += 0.01;
    this.x += 15;
    this.y = perlinValue * 1500;
  }
  
  posibilidad() {
    //pasos "normales" - POSIBILIDAD
    let choice = floor(random(4));

    if (choice == 0) {
      this.x+=15;
    } else if (choice == 1) {
      this.x-=15;
    } else if (choice == 2) {
      this.y+=15;
    } else {
      this.y-=15;
    }
  }

  excepcion() {
    //implementación levy flight - EXCEPCIÓN
    let r = random(1);
    if (r < 0.02) {
      let step = 300;
      let stepx = random(-step, step);
      let stepy = random(-step, step);
      this.x += stepx;
      this.y += stepy;
    } else {
      this.x += random(-10, 10);
      this.y += random(-10, 10);
    }
  }

  muerte()
  {

    this.x += random(-5, 5);
    this.y += random(-5, 5);

    if (millis() - this.tiempoCorrupcion > this.tiempoRecuperacion) {
      this.modo = this.modoOriginal;
      this.r = 5; 
    }
  }
}

function keyPressed() {
  if (key === 'e') {
    radii = 0;
    eraseScreen = true;
    walkers = [];
  }
    /*
  else if(keyCode === 39) {
    for (let w of walkers) {
      w.modo++;
      if (w.modo > 4) w.modo = 1;
    }
  }
  else if(keyCode === 37) {
    for (let w of walkers) {
      w.modo--;
      if (w.modo < 1) w.modo = 4;
    }
  }
  */
}

function mousePressed() {
  let nuevoWalker = new Walker(modo);
  nuevoWalker.x = mouseX;
  nuevoWalker.y = mouseY;
  
  walkers.push(nuevoWalker);
  
  modo++;
  if (modo > 4) {
    modo = 1;
  }
}
```
Ahora le pediré a una IA que ponga la palabra reservada donde necesita. Una vez hecho eso, ya funciona de maravilla, y ya puedo dibujar cosas SIN RASTRO, lo cual hubiese sido excelente para la parte de opacidad de las instrucciones... no lo había pensado. MI LOGICA SI ERA CORRECTA SOLO QUEAJ lfka kjhfk JHGFkj hgajkhfgaygfafhjbgaghjkghjkhjgakfhjgaghjksghjkagfhgkGKgkafgakghfghj VOY A CHILLAR.

Ahora falta la parte importante de afectar probabilidades cuando EL USUARIO está presente, no me gusta lo que propuso la IA entonces voy a hacer un if que si mousex y mouse son 0 o están por fuera de la pantlla entonces no hace nada.

Para lograr eso lo que hice fue poner en cada uno de los comportamientos un if que solo deja pasar si el mouse está en la pantalla, a partir de esto, en cada uno de los comportamientos creé variables que son inicializadas con un valor pero si se cumple que el mouse está dentro de la pantalla entonces las cambia para que el movimiento sea más errático.

```js
tendencia() {
    //pasos "normales" - POSIBILIDAD
    let limite = 8;  
    let paso = 15;   

    if(mouseX != 0 && mouseX > 0 && mouseX < width && mouseY != 0 && mouseY > 0 && mouseY < height) {
      limite = 5; 
      paso = random(10, 30); 
    }
    
    let choice = floor(random(limite));

    if (choice == 0) {
      this.x += paso;
    } else if (choice == 1) {
      this.x -= paso;
    } else if (choice == 2) {
      this.y += paso;
    } else {
      this.y -= paso;
    }
  }
  
  normalidad() {
    let incrementoT = 0.01; 
    let pasoX = 15;         

    if(mouseX != 0 && mouseX > 0 && mouseX < width && mouseY != 0 && mouseY > 0 && mouseY < height) {
      incrementoT = random(0.05, 0.15); 
      pasoX = random(5, 25);            
    }
    
    let perlinValue = noise(this.t);

    //====== INCREMENTO VARIABLES=========
    this.t += incrementoT;
    this.x += pasoX;
    this.y = perlinValue * 1500;
  }
  
  posibilidad() {
    //pasos "normales" - POSIBILIDAD
    let paso = 15; 

    if(mouseX != 0 && mouseX > 0 && mouseX < width && mouseY != 0 && mouseY > 0 && mouseY < height) {
      paso = random(2, 45); 
    }
    
    let choice = floor(random(4));

    if (choice == 0) {
      this.x += paso;
    } else if (choice == 1) {
      this.x -= paso;
    } else if (choice == 2) {
      this.y += paso;
    } else {
      this.y -= paso;
    }
  }

  excepcion() {
    //implementación levy flight - EXCEPCIÓN
    let probabilidadSalto = 0.02; 
    let ruidoBase = 10;           

    if(mouseX != 0 && mouseX > 0 && mouseX < width && mouseY != 0 && mouseY > 0 && mouseY < height) {
      probabilidadSalto = 0.15; 
      ruidoBase = 30;           
    }
    
    let r = random(1);
    if (r < probabilidadSalto) {
      let step = 300;
      let stepx = random(-step, step);
      let stepy = random(-step, step);
      this.x += stepx;
      this.y += stepy;
    } else {
      this.x += random(-ruidoBase, ruidoBase);
      this.y += random(-ruidoBase, ruidoBase);
    }
  }
```
| Criterio | Cumplo | No cumplo | Evidencia |
| :--- | :---: | :---: | :--- |
| **Encargo completo:** interpreto los cinco momentos dentro de un mismo sistema visual. | X | | [evidencia 1](#e1)|
| **Simulación con intención:** utilizo al menos tres conceptos de la unidad para comunicar las ideas del encargo. | X | | [evidencia 2](#e2)|
| **Interacción significativa:** la interacción modifica el comportamiento o las probabilidades del sistema, que también funciona sin intervención. | X | |[evidencia 3](#e3)|
| **Prototipo funcional:** la experiencia puede ejecutarse y recorrerse completa sin errores que impidan comprenderla. | X | | [evidencia 4](#e4)|
| **Proceso documentado:** la bitácora evidencia avances, decisiones, dificultades, soluciones, uso de IA y enlace al prototipo. | X | | [evidencia 5](#e5)|
