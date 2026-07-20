# UNIDAD 1: ALETORIEDAD
## Actividad 1

Despues de observar los videos y leer los ensayos de Tyler Hobbs comprendo que el concepto de *Aletoriedad* en el arte es para que el producto final sea distinto cada vez que se iter.

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

## Actividad 3

1.) En tus propias palabras cuál es la diferencia entre una distribución uniforme y una no uniforme de números aleatorios.

Una distribución uniforme tiene la misma probabilidad de generar todos los números en un rango. Una distribución no uniforme tiene mayor probabilidad en algunos valores, en el caso de la distribución gaussiana, este tiene mayor probabilidad de generar los valores que están cerca de la media.

2.) Modificar el código para que tenga mayor probabilidad de moverse a la derecha.

Lo que hice fue utilizar randomGaussian() para que la probabilidad de generar valores cercanos a 0 sea mayor

```py
let choice = floor(randomGaussian(0,3));
    if(choice < 0)
    {
      choice = 0;
    }
```
<img width="700" height="700" alt="image" src="https://github.com/user-attachments/assets/ebb46080-b11f-4ef9-b143-7e65e1f01755" />

3.) otras cosas

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

El código del ejercicio:

```
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
