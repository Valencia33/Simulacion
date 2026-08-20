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
