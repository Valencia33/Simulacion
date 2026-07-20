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
