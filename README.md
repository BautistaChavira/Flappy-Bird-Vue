Este mini  proyecto es una copia descarada del clásico minijuego flappy bird, pero hecho con vue.

<img width="689" height="455" alt="image" src="https://github.com/user-attachments/assets/a56ced5d-f24e-4d30-af0c-0a7c33e54a8d" />

El juego no comienza hasta que no das el primer click.

El proyecto esta construido con Vite y Vue.

El corazón del proyecto esta en src,  App.vue y main.js. 

El proyecto está dividido en componentes donde toda la lógica la maneja el Game.vue y los componentes Bird y Pipe solo se usan para renderizar las figuras en la pantalla, realmente toda la lógica la maneja el Game.vue.

El juego no carga assets, de hecho no tiene un directorio de assets como tal.

Aspectos como el repetirse cuando pierdes, la puntuación y las colisiones, la mayoría esta en methods, puse demasiados comentarios para tratar de facilitar la modificación.

<img width="948" height="765" alt="{1FE4D933-BDE3-4503-9243-18EBEC3BCA54}" src="https://github.com/user-attachments/assets/7aa1f363-1b49-4e07-b16e-acfd4f93333a" />

Las colisiones estan hardcodeadas con números mágicos (lo siento), esto quiere decir que si quieres cambiar la resolución o el tamaño del lienzo tendrás que mover un montón de valores. No es imposible pero sí será muy tedioso.

El despliegue en Railway fue prácticamente automático, no fue necesario mover comandos de inicio.

Si tú quieres desplegarlo en forma de host local desde tu máquina solo descarga el proyecto, instala las dependencias con npm install y córrelo como un servidor de pruebas con npm run dev.
