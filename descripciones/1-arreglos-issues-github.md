Arreglos pequeños de issues abiertas, sobre tu main (5c97df2). **Ninguno añade lecturas ni escrituras a Firebase.**

| Issue | Arreglo | Archivo |
|---|---|---|
| #263 | Las bolas de experiencia y los objetos atraídos van siempre a 1,4 veces tu velocidad como mínimo, así que ya no se quedan atrás. Es el mismo cambio que la PR #294 de zjkung1123, que se nombra en la entrada de Novedades propuesta. | `js/entities/pickup.js` |
| #353 | Capa Tóxica envenena a quien te golpea cuerpo a cuerpo. Corrosión da +20 % a los ataques de tipo Veneno. Antes las dos caían en el +8 % genérico. Se reutilizan textos que ya estaban traducidos. | `js/data/ability-fx.js` |
| #320 | La cuenta atrás «Se renuevan en» se calcula con la hora de Europe/Madrid, que es cuando cambian de verdad las misiones y la tienda. La semanal, además, iba un día desfasada: el lunes marcaba 1 día en vez de 7. | `js/ui/goals-ui.js` |
| #333 | `autocapitalize="none" autocorrect="off"` en los campos del apodo propio y del apodo del amigo, igual que en el login el 26-10. | `dev.html` |
| #262, #246, #298 | Si algo falla al montar las cartas de nivel o al aplicar la elegida, el juego vuelve al estado `playing` y la partida no se queda congelada. Cuando no hay fallo, nada cambia. | `js/game.js` |

## Antes y después

### #320: cuenta atrás de las misiones

Un jugador en Brasil a las 19:24, cuando en España son las 23:24. Las misiones cambian a las 00:00 de España, es decir, dentro de 36 minutos.

- **Antes:** las diarias marcaban «4 h 36 min» y las semanales «6 d 4 h».
- **Después:** las diarias marcan «0 h 36 min» y las semanales «5 d 0 h».

| Antes | Después |
|---|---|
| ![#320 antes](https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/issues-github/bug320-antes.png) | ![#320 después](https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/issues-github/bug320-despues.png) |

### #353: habilidades de Glimmora

Las dos habilidades se muestran juntas para compararlas; en la ficha real sólo sale la que tiene el Pokémon.

![#353 antes](https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/issues-github/bug353-antes.png)
![#353 después](https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/issues-github/bug353-despues.png)

## Pruebas

Pasan todos los tests (`node --test tests/*.test.cjs`) y `node tools/build.js` compila sin errores. `dev.html` carga en Chromium sin errores de página y las dos habilidades tienen su efecto.

## Novedades propuestas

No lleva entrada en Novedades: eso te lo dejo a ti. Por si te sirve, esto es lo que pondría (tengo también las traducciones a los otros 5 idiomas, si las quieres):

**Arreglos (`fix`)**

- La experiencia y los objetos que atraes ya te alcanzan aunque vayas muy rápido (mejoras, buffs o clima): antes se quedaban atrás y no llegaban hasta que parabas. Gracias a zjkung1123 por el arreglo.
  - _EN:_ Experience and items you pull in now catch up with you even when you are very fast (upgrades, buffs or weather): they used to fall behind and only arrived when you stopped. Thanks to zjkung1123 for the fix.
- Las habilidades Capa Tóxica y Corrosión ya tienen su propio efecto: con Capa Tóxica, quien te golpea cuerpo a cuerpo se envenena; con Corrosión, +20 % de daño con movimientos de tipo Veneno. Antes las dos daban sólo un pequeño extra de daño (Glimmora tenía dos habilidades iguales).
  - _EN:_ The Toxic Debris and Corrosion abilities now have their own effect: with Toxic Debris, whoever hits you in melee gets poisoned; with Corrosion, +20% damage with Poison-type moves. Before, both only gave a small damage bonus (Glimmora had two identical abilities).
- Misiones: la cuenta atrás de «Se renuevan en» va ya con la hora de España, que es cuando cambian las misiones y la Tienda Kecleon. Fuera de España llegaba a cero y no pasaba nada; y la de las semanales iba un día desfasada.
  - _EN:_ Missions: the "Refresh in" countdown now follows Spain time, which is when missions and the Kecleon Shop change. Outside Spain it reached zero and nothing happened; and the weekly one was a day off.
- Móvil: al escribir tu apodo o el de un amigo, el teclado ya no lo corrige ni le pone mayúsculas por su cuenta (salía «No hay ningún jugador con ese apodo»).
  - _EN:_ Mobile: when you type your nickname or a friend's, the keyboard no longer autocorrects it or adds capitals on its own (you got "There is no player with that nickname").
- Si algo fallaba al elegir una carta de nivel, la partida se quedaba congelada para siempre (el tiempo y los enemigos parados, sin poder pausar). Ahora la partida sigue.
  - _EN:_ If something went wrong when picking a level-up card, the run froze forever (time and enemies stopped, no way to pause). Now the run keeps going.


## Para fusionarla

Hay cuatro PRs más con el mismo formato: bugs de X, mejoras de X, Olvidamovimientos e interfaz. Cada una es un solo commit sobre tu main con sólo el código fuente (sin index.html, app.min.js, version.json, js/lang ni páginas), para que puedas fusionarla con el botón y publicar con tu build de siempre. Si al fusionar una se descuadra otra, la pongo yo al día. Y si algo no te convence, cámbialo o dímelo y lo ajusto.

Un detalle sin importancia, sólo si te viene bien: si al adaptar alguna haces un commit tuyo, ¿podrías añadir al final esta línea? Así GitHub me cuenta como colaborador, que me haría ilusión.

```
Co-authored-by: Kiev <246354800+kiev-amaterasu@users.noreply.github.com>
```

¡Gracias por el juego!
