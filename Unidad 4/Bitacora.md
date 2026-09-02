# Unidad 4

**1.) Leí y verifiqué que mi proyecto cumple con los requisitos mínimos de la unidad: 25 puntos.**

- 8 agentes simultáneos gobernados por el sistema dinámico.

Existen 8 agentes y cada uno tiene asociado un instrumento y una imagen (o al menos hasta ahora ese es el plan), el instrumento es gobernado por varios parametros como K, w, el tempo, el volumen y en que modo esté. En cuanto la imagen, y esto ya es conceptualización pq aún ni idea de como hacerlo, pero tengo pensado que cada uno tenga una imagen asociada a un dibujo hecho con ASCII characters y los cuales se verán afectados dependiendo del acoplamiento individual de cada pista. Cada agente tiene la opción de ser gobernado por Kuramoto o si tener un tempo fijo.

- 4 personalidades audiovisuales diferentes.

Habrán al menos 8, puesto que cada agente en realidad es una personalidad audiovisual diferente, por lo que realmente termino teniendo el doble.

- Cada agente deberá tener una manifestación visual y una manifestación sonora vinculadas a su comportamiento.

>> Existen 8 agentes y cada uno tiene asociado un instrumento y una imagen (o al menos hasta ahora ese es el plan), el instrumento es gobernado por varios parametros como K, w, el tempo, el volumen y en que modo esté. En cuanto la imagen, y esto ya es conceptualización pq aún ni idea de como hacerlo, pero tengo pensado que cada uno tenga una imagen asociada a un dibujo hecho con ASCII characters y los cuales se verán afectados dependiendo del acoplamiento individual de cada pista. Cada agente tiene la opción de ser gobernado por Kuramoto o si tener un tempo fijo.

Dicho esto se da a entender cual será la manifestación visual y sonora vinculada a cada uno.

- El usuario deberá poder modificar en tiempo real al menos 2 variables relacionadas con el modelo, siendo obligatorio poder intervenir (K).

El usuario puede modificar K, w, el tempo, el volumen HASTA ESTE MOMENTO DEL DISEÑO, tengo planeado que pueda hacer más cosas cuando implemente la parte de las visuales pero hasta ahora no lo he hecho.

- Deberán existir al menos 2 formas diferentes de interacción performativa, una que afecte el comportamiento global del sistema y otra que permita intervenir agentes individuales.

Hay que mirarlo más a fondo y de pronto con más iteraciones será posible tenerlo más claro, pero en este momento lo que es w, K y el tempo son variables que tienen efectos GLOBALES. Lo que se me ocurre para lograr que sea más personalizable es manejar cada agente individualmente desde el dibujo.

- Deberá existir al menos 1 mecanismo de perturbación que permita alterar el estado de uno o varios agentes y observar posteriormente la respuesta del colectivo.

Esto lo quiero lograr desde la parte visual, pues me imagino un dibujo como en otra tab que esté compuesto por particulas que se puedan desorganizar peor que tiendan al orden, de esta forma es posible, que haga un calculo de la distancia original de una particula a su estado actual y de esa forma calcular una especie de variable global que interactue con el K, y se le reste, capeado a 0.

- La experiencia deberá permitir reconocer al menos 3 estados colectivos: desorden, organización parcial y organización estable.

Esto lo estoy logrando a partir de la formula que el profe mostró en clase y multiplicando por 100, de esta forma podemos calcular y crear intervalos en los que consideremos que está desornado, organizado parcialmente o completamente estable.

- Deberá existir al menos 1 forma perceptible de comunicar el estado colectivo. Puede ser visual, sonora, audiovisual o mediante un indicador explícito.

Tengo un indicador explicito, sin embargo estoy seguro de que si no existiera igual sería posible definir en que estado está la aplicación.

**Puedo explicar claramente qué representa cada variable del modelo de Kuramoto en mi proyecto: 25 puntos.**
