Tres mejoras que te propusieron los jugadores en X, sobre tu main (5c97df2). Ninguna añade lecturas ni escrituras en Firebase.

## Cambios

- **Avisos de shiny más visibles** (@RyuKOTAQ: «casi nunca veo el mensaje ni de que apareció un Shiny, ni de que lo derrote»):
  - «¡Un X shiny anda cerca!» y «¡Has conseguido a X shiny!» tienen el mismo estilo que los demás avisos, pero en azul shiny, un poco más grandes, con un destello a cada lado, y duran 4,5 s.
  - Ningún aviso normal los pisa: antes, cualquier mensaje posterior («¡Marea de Pokémon!», un bioma, una esfera…) sustituía al del shiny. Ahora el normal espera a que acabe y sale después.
  - Archivos: `spawner.js` (`say(text, secs, local, shiny)`), `hud.js` y `game.js`.
  - Cooperativo: el anfitrión manda la marca como 4.º campo de `'say'` (`coop.js`). Los clientes de la versión anterior lo ignoran, así que no se rompe nada.
- **Vuelta de la grieta protegida**: al volver se cae donde se entró, muchas veces en medio de la horda.
  - Ahora hay **1 s de invulnerabilidad** y un **empujón suave** (unos 50 px, radio de 130 px) a los enemigos que esperaban ahí, más un anillo que lo marca (`rift.js` `finish`).
  - Al empujón no le afectan jefes ni Arceus. Lo aplica quien manda a los enemigos (el anfitrión en cooperativo).
- **Botón «Mejora total»** (@kiuki_pls: «un botón que sea maxear todas a la vez y que se vea cuánto cuesta»):
  - En Mejoras, a la derecha de la cabecera (en móvil, debajo y a todo lo ancho), el botón enseña lo que cuesta subir todas las mejoras de ese Pokémon. Si no llega, también dice cuánto falta.
  - Antes de gastar nada abre una ventana con cada mejora (nivel actual → nuevo), el precio total, las monedas que te quedan y «No se puede deshacer».
  - Si no llega para todo, compra lo que pueda empezando por lo más barato y lo dice claramente.
  - Al confirmar, se recalcula con la partida de ese momento.
  - Archivos: `menu.js` (`upgradePlan`, `upgradeAllButton`), `dev.html` (`#upg-all`) y `style.css` (`.upg-all`). Los textos nuevos van en los 7 idiomas (`lang-en.js`, `lang-updates.js`).

## Antes y después

### Aviso de shiny (sale un shiny y, medio segundo después, «¡Marea de Pokémon!»)
| Antes: la marea tapa el aviso del shiny | Después: el shiny se queda y destaca |
|---|---|
| <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/mejoras-x/shiny-antes-1.png" width="420"> | <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/mejoras-x/shiny-despues-1.png" width="420"> |

Cuando acaba el del shiny sale el que esperaba:

<img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/mejoras-x/shiny-despues-2.png" width="420">

### Vuelta de la grieta
Medido en Chromium con 30 enemigos esperando en la entrada. **Antes**: invulnerabilidad 0 al volver. **Después**: 1 s, y quedan 0,67 s a los 0,25 s. El anillo marca el empujón:

<img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/mejoras-x/grieta-despues-1.png" width="420">

### Mejora total
| Botón con el precio total | Confirmación (hay monedas para todo) | Hecho |
|---|---|---|
| <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/mejoras-x/full-01-boton.png" width="300"> | <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/mejoras-x/full-02-confirmar-todo.png" width="300"> | <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/mejoras-x/full-03-hecho.png" width="300"> |

Si no llega para todo (Pikachu con 3.000 monedas):

| Botón con lo que falta | Confirmación parcial | En móvil |
|---|---|---|
| <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/mejoras-x/full-04-sin-monedas.png" width="300"> | <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/mejoras-x/full-05-confirmar-parcial.png" width="300"> | <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/mejoras-x/full-06-movil.png" width="240"> |

## Pruebas

- Pasan todos los tests, incluida la nueva `tests/banner.test.cjs` (el shiny no se pisa, el normal sale después, otro shiny sí lo sustituye y el anfitrión manda la marca). `node tools/build.js` compila sin errores (`build_langs.js --faltan`: 0 en cada idioma).
- Las tres mejoras se han probado en Chromium con Playwright, en modo local (sin tocar el Firebase de producción), sin errores de consola.
- **Falta probar el cooperativo con dos aparatos:** que el invitado vea el aviso de shiny en azul sin que lo tape otro aviso, que un invitado con la versión anterior lo vea como siempre y sin errores, y que al volver de una grieta los dos tengan el segundo de protección.

## Novedades propuestas

No lleva entrada en Novedades. Por si te sirve:

**Nuevo (`new`)**

- Mejoras: botón «Mejora total», con lo que cuesta subir todas las mejoras de ese Pokémon. Antes de gastar nada te enseña qué niveles se compran, cuánto cuesta y con cuántas monedas te quedas. Si no te llega para todo, compra lo que puedas empezando por lo más barato.
  - _EN:_ Upgrades: a «Full upgrade» button that shows what it costs to max all of that Pokémon's upgrades. Before spending anything it shows which levels you buy, what it costs and how many coins you will have left. If you cannot afford everything, it buys what it can, cheapest first.

**Cambios (`chg`)**

- Avisos de shiny más visibles: salen en azul shiny, con un destello a cada lado y durante más tiempo. Y ningún otro aviso los tapa: antes, con mucho jaleo en pantalla, el del shiny se pisaba y no te enterabas de que había aparecido ni de que lo habías conseguido.
  - _EN:_ Shiny alerts are easier to see: in shiny blue, with a sparkle on each side and for longer. And no other alert covers them: before, with a lot going on, the shiny alert got overwritten and you did not notice that one had appeared or that you had caught it.
- Al volver de una grieta tienes 1 segundo sin recibir daño y los enemigos que esperaban justo donde entraste se apartan un poco. Antes caías en medio de la horda y te comías los golpes sin poder hacer nada.
  - _EN:_ When you come back from a rift you get 1 second without taking damage, and the enemies waiting right where you went in are pushed back a little. Before, you landed in the middle of the horde and took hits you could do nothing about.


---

Mismo formato que la de arreglos de issues: un commit sobre tu main, sólo código fuente, se puede fusionar con el botón.
