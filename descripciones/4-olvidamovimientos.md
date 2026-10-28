Nuevo objeto, el **Olvidamovimientos**, para que un Pokémon olvide un movimiento aprendido con MT (lo pidieron 4 personas en X). Va sobre tu main (5c97df2) y no añade lecturas ni escrituras en Firebase: sólo un campo más en el guardado, que se sube igual que antes. De paso, la Mochila ya no se mete debajo de la barra de arriba.

## Cambios

- **Objeto en la Tienda Kecleon** (`js/data/shop.js`):
  - Cuesta 1500 monedas, como la Menta, y va a la Mochila y a la libreta de monedas como los demás objetos.
  - Texto: «Un Pokémon olvida un movimiento aprendido con MT (los suyos propios, no). Podrá volver a aprenderlo.»
  - Lleva su propio icono pixel art: un disco de MT gris tachado en rojo (`js/ui/icons.js`).
  - También está en la estantería de Kecleon y en el texto de la Mochila (`js/ui/shop-ui.js`).
  - Orden de los objetos, en la tienda y en la Mochila: Olvidamovimientos, Menta, Cápsula Habilidad y Cápsula Habilidad Oculta (`Shop.ORDER`).
  - Los cuatro objetos de la tienda van en una sola fila, con el precio debajo del texto, para que no quede un hueco vacío (`.upg-4` en `style.css`; en pantallas estrechas pasan a 2 columnas y en móvil a 1).
- **En la ficha del Pokémon** (`js/ui/menu.js`), igual que la Menta:
  - El botón «Olvidar MT ×N» aparece junto a «Enseñar MT» si el Pokémon tiene alguna MT aprendida y tienes Olvidamovimientos.
  - Al pulsarlo se abre la lista de **sólo los movimientos aprendidos con MT**, con un aviso arriba: «¿Qué movimiento aprendido con MT olvida? Se gasta un Olvidamovimientos. Sus movimientos propios no se pueden olvidar».
  - Al elegir uno se gasta el objeto y sale un aviso: «X ha olvidado Y. Puede volver a aprenderlo con su MT».
- **Los movimientos propios no se pueden olvidar:** `G.Mons.forget(dex, id)` (`js/systems/mons.js`) sólo acepta movimientos de `taught(dex)`, la lista de MT aprendidas.
- **No es para siempre:** lo olvidado vuelve a salir en «Enseñar MT» y se puede aprender otra vez con su MT, y olvidarlo de nuevo, todas las veces que se quiera.
- **Fusión entre aparatos** (`js/core/db.js`):
  - Hasta ahora las MT se unían y nunca se quitaban, así que una MT olvidada habría vuelto al juntar la partida con otro aparato.
  - Ahora cada MT apunta cuándo se aprendió (1) o se olvidó (0) en `save.ptmAt[dex][mov] = [1|0, fecha]`, y al fusionar manda lo último que pasó en cualquiera de los dos aparatos.
  - Las partidas sin fechas (las de antes) siguen con la unión de siempre. `save.ptm` mantiene su formato, así que la versión anterior lo sigue leyendo bien.
- **Mochila debajo de la barra de arriba** (`style.css`): `#scr-bag` no estaba en la lista de pantallas que empiezan debajo de la barra (66 px, 92 px en ventanas estrechas), así que el título y «Volver» quedaban tapados. Ahora empieza como la Tienda y las demás.
- Los textos nuevos van en los 7 idiomas (`lang-en.js`, `lang-updates.js`).

## El proceso, paso a paso

| 1. En la Tienda Kecleon | 2. Comprado | 3. En la Mochila |
|---|---|---|
| <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/olvidamovimientos/1-tienda.png" width="300"> | <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/olvidamovimientos/2-comprado.png" width="300"> | <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/olvidamovimientos/3-mochila.png" width="300"> |

| 4. Ficha con dos MT aprendidas: «Olvidar MT ×1» | 5. Elegir cuál (sólo las de MT) | 6. Olvidada: vuelve «Enseñar MT» |
|---|---|---|
| <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/olvidamovimientos/4-ficha-con-mt.png" width="300"> | <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/olvidamovimientos/5-elegir-cual-olvida.png" width="300"> | <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/olvidamovimientos/6-olvidada.png" width="300"> |

| 7. Volver a enseñarla con su MT | 8. Aprendida otra vez | Tienda en móvil |
|---|---|---|
| <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/olvidamovimientos/7-ensenar-de-nuevo.png" width="300"> | <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/olvidamovimientos/8-aprendida-otra-vez.png" width="300"> | <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/olvidamovimientos/1b-tienda-movil.png" width="220"> |

Guardado durante la prueba (Charizard con Terratemblor y Garra Dragón):
- Al olvidar: `ptm = ["dragon-claw"]`, `ptmAt.bulldoze = [0, …]`, y quedan 0 Olvidamovimientos.
- Al reaprender: `ptm = ["dragon-claw","bulldoze"]` y `ptmAt.bulldoze = [1, …]`.

### Mochila
| Antes: el título, «Volver» y el texto quedan bajo la barra | Después: empieza debajo, como la Tienda |
|---|---|
| <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/olvidamovimientos/bag-antes.png" width="420"> | <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/olvidamovimientos/bag-despues.png" width="420"> |

## Pruebas

- Pasan todos los tests, con una nueva en `tests/db.test.cjs`: lo olvidado en un aparato no vuelve al juntar con otro que no se había enterado; volver a aprenderla después gana; olvidarla otra vez la vuelve a quitar; sin fechas, sigue la unión de siempre. `node tools/build.js` compila sin errores (`build_langs.js --faltan`: 0 en cada idioma).
- Todo el proceso se ha probado en Chromium con Playwright, en modo local (sin tocar el Firebase de producción), sin errores de consola.
- Un detalle: si una pestaña con la versión anterior abierta guarda encima, puede perder el campo `ptmAt`. El actualizador recarga a los jugadores fuera de partida, así que es raro, y en el peor caso la MT olvidada volvería a aparecer.

## Novedades propuestas

No lleva entrada en Novedades. Por si te sirve:

**Nuevo (`new`)**

- Nuevo objeto en la Tienda Kecleon: el Olvidamovimientos (1500 monedas, como la Menta). En la ficha del Pokémon, «Olvidar MT» te deja elegir qué movimiento aprendido con MT olvida; sus movimientos propios no se pueden olvidar. No es para siempre: lo puede volver a aprender con su MT y olvidarlo otra vez, y lo olvidado no reaparece al jugar en otro aparato.
  - _EN:_ New item in the Kecleon Shop: the Move Deleter (1500 coins, like the Mint). On the Pokémon's card, «Forget TM» lets you choose which TM move it forgets; its own moves cannot be forgotten. It is not forever: it can learn the move again with its TM and forget it again, and a forgotten move does not come back when you play on another device.

**Arreglos (`fix`)**

- La Mochila ya no se mete debajo de la barra de arriba: empieza más abajo, como la Tienda Kecleon y las demás ventanas.
  - _EN:_ The Bag no longer slips under the top bar: it now starts lower, like the Kecleon Shop and the other windows.


---

Mismo formato que la de arreglos de issues: un commit sobre tu main, sólo código fuente, se puede fusionar con el botón.
