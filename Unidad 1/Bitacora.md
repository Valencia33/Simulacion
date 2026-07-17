# UNIDAD 1: ALETORIEDAD
## Actividad 1

Despues de observar los videos y leer los ensayos de Tyler Hobbs comprendo que el concepto de *Aletoriedad* en el arte es para que el producto final sea distinto cada vez que se iter.

```
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
