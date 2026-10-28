Mejoras de interfaz, sobre tu main (5c97df2). Son cambios discretos que reutilizan los estilos que ya tiene el juego (recuadros, chips y colores del HUD). **No añaden lecturas ni escrituras a Firebase.**

## Qué cambia

| | Cambio | Archivos |
|---|---|---|
| 1 | **Cartas de mejora siempre a la vista.** Antes solo salían en la pausa. En el ordenador van a la izquierda del objeto, en parejas (una encima de otra), y si sobra una suelta va la primera por la izquierda (Aprendizaje si la tienes). Llevan icono y ×N, y con el ratón encima un cartel dice qué hace la carta (el mismo estilo que el de las esferas). En el móvil van en una columna pegada al borde izquierdo, a media altura, porque abajo las taparía el dedo. Las que están al máximo salen en dorado. La Baya Zidra no aparece porque se gasta al cogerla. | `js/ui/hud.js` |
| 2 | **Bioma, derrotados y monedas.** En el ordenador pasan de la línea gris de 10 px bajo el reloj a un recuadro a la derecha de los ataques. En el móvil van a la derecha del reloj, en la misma línea, para no robar altura (si hay clima activo y no caben, vuelven debajo del reloj). Los números llevan icono, así que ya no aparece «1 monedas». | `js/ui/hud.js` |
| 3 | **Barra del jefe (solo ordenador).** Pasa de 12 a 18 px de alto, y el nombre se escribe en blanco con borde. En el móvil se queda la de siempre, que en pantalla pequeña se ve mejor. | `js/ui/hud.js` |
| 4 | **Misiones en el menú principal.** En pantallas anchas (≥1200×661) se muestran a la izquierda, con su progreso y el botón «Recoger». Al pulsar el recuadro se abre Misiones. En pantallas más pequeñas no se muestran. | `js/ui/goals-ui.js`, `js/ui/menu.js`, `dev.html`, `css/style.css` |
| 5 | **Fondo para Novedades y YouTube**, como el que ya tienen las monedas. Antes los Pokémon del menú pasaban por detrás y no se leían. | `css/style.css` |
| 6 | **Mejoras.** El precio va siempre en una línea (antes, en algunas tarjetas la moneda quedaba encima del número y los botones tenían tamaños distintos), y el selector de Pokémon usa una flecha dorada en vez de la del navegador. | `js/ui/menu.js`, `css/style.css` |

No hay textos nuevos: se reutilizan los que ya estaban traducidos.

## Antes y después

**HUD de abajo (1920×1080)**
![HUD abajo](https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/interfaz/comparativa-1-hud-abajo.png)

**Cartel al pasar el ratón por una carta**
![Cartel](https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/interfaz/desktop-carta-raton-encima.png)

**Barra del jefe (ordenador)**
![Jefe](https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/interfaz/comparativa-2-jefe-arriba.png)

**Partida entera**
![Partida](https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/interfaz/comparativa-3-partida-entera.png)

**Móvil (844×390)**
![Móvil](https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/interfaz/comparativa-5-movil-partida.png)

**Menú principal**
![Menú](https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/interfaz/comparativa-4-menu.png)

**Novedades y YouTube**
![Botones](https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/interfaz/comparativa-6-botones-arriba.png)

**Mejoras**
![Mejoras](https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/interfaz/propuesta-mejoras-comparativa.png)

## Pruebas

Pasan todos los tests y `node tools/build.js` compila sin errores. Probado en Chromium a 1920×1080 y en móvil 844×390 sin errores de página: «Recoger» desde el menú da el premio y no abre la pantalla de Misiones, el recuadro sí la abre, y el cartel de las cartas aparece al pasar el ratón.

Toca `js/ui/hud.js`, igual que la PR de mejoras de X (avisos de shiny). Si fusionas aquella antes, pongo esta al día.

## Novedades propuestas

No lleva entrada en Novedades. Por si te sirve:

**Cambios (`chg`)**

- En partida, las cartas de mejora que llevas (Potencia, Carrera, Imán, Aprendizaje…) se ven siempre: en el ordenador, a la izquierda de los ataques (con el ratón encima te dice qué hace cada una); en el móvil, en columna pegadas al borde izquierdo. Antes sólo salían en la pausa. Las que tienes al máximo, en dorado.
  - _EN:_ In a run, the upgrade cards you have (Power, Sprint, Magnet, Learning…) are always on screen: on computer, to the left of your moves (hover one to see what it does); on mobile, in a column along the left edge. They used to show only in the pause screen. Maxed ones are gold.
- El bioma, los Pokémon derrotados y las monedas pasan de la línea pequeña bajo el reloj a un recuadro a la derecha de los ataques (en el móvil, a la derecha del reloj), con iconos y más grande. (De paso, ya no pone «1 monedas».)
  - _EN:_ The biome, defeated Pokémon and coins move from the small line under the timer to a box to the right of your moves (on mobile, to the right of the timer), with icons and bigger. (And it no longer says "1 coins".)
- En el ordenador, la barra de vida de los jefes es más gruesa y su nombre se lee mejor.
  - _EN:_ On computer, the boss health bar is thicker and its name is easier to read.
- Menú principal: en pantallas anchas, tus misiones salen a la izquierda, con su progreso y el botón «Recoger». Al tocar el recuadro, se abren Misiones.
  - _EN:_ Main menu: on wide screens, your missions show on the left, with their progress and the "Claim" button. Click the box to open Missions.
- Los botones Novedades y YouTube tienen fondo, como el resto de la barra: los Pokémon del menú ya no pasan por detrás y los tapan.
  - _EN:_ The News and YouTube buttons now have a background, like the rest of the bar: the menu Pokémon no longer walk behind them and cover them.
- Mejoras: el precio va siempre en una línea (antes, en algunas la moneda quedaba encima del número) y el selector de Pokémon tiene el estilo del juego.
  - _EN:_ Upgrades: the price is always on one line (in some, the coin used to sit above the number) and the Pokémon picker matches the game's style.


---

Mismo formato que la de arreglos de issues: un commit sobre tu main, sólo código fuente, se puede fusionar con el botón.
