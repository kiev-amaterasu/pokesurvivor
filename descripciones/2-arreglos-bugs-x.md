Arreglos de bugs que los jugadores te reportaron en X, sobre tu main (5c97df2). Ningún cambio añade lecturas ni escrituras en Firestore.

Los bugs de las monedas en la barra, las Mentas en móvil, el clima de los invitados y el gacha con mando ya estaban arreglados en 5c97df2, así que no van aquí.

## Cambios

- **Shiny en móvil horizontal** (`css/style.css`): en la ficha de la Pokédex, el selector Normal/Shiny se encogía a una raya de 4 px (flex con scroll y `overflow:hidden`) y no se podía tocar. Ahora los hijos de `#dex-detail` no se encogen.
- **Cooperativo: cambio de Pokémon** (`js/ui/menu.js`, `js/net/social.js`): la sala solo se enteraba del compañero al abrir la pantalla de sala. Ahora se avisa al elegir compañero o al cambiar entre normal y shiny. `refreshMember()` solo escribe si algo cambió: ~22 bytes en la Realtime Database por cambio, y solo estando en sala.
- **Grietas: Pokémon perdido** (`js/systems/events.js`): su temporizador (120 s) seguía corriendo durante la grieta (120 s) y te seguía hacia la arena, así que casi siempre se iba. Ahora espera fuera, no se dibuja en la arena y al volver aparece a tu lado. En cooperativo decide el anfitrión, sin mensajes nuevos.
- **Sonido saturado en móvil** (`js/core/audio.js`): limitador final, ganancias algo más bajas y tope de voces que se libera cuando el sonido termina de verdad (antes, a los 150 ms). El tope es de 14 voces en táctil y 24 en ordenador. Con el volumen al máximo, el pico baja de 1,27 a 0,94 y ya no hay recortes.
- **FPS con niebla y en la Sentencia** (`js/core/util.js` `G.U.veil`, `game.js`, `world.js`, `weather.js`, `judgment.js`): la viñeta, la niebla y el velo de la Sentencia se pintaban con degradados a pantalla completa en cada fotograma. Ahora se pintan una vez y se copian. La rueda de Arceus se guarda en un sprite. Con niebla y la CPU ×4 sube de 36-39 a 57-59 fps; la Sentencia, de 27 a 50 fps. Se ve igual: comparado píxel a píxel, la diferencia máxima es de 3/255.
- **Alto contraste para daltónicos** (`js/systems/hazards.js`, `settings.js`, `settings-ui.js`): nuevo ajuste «Avisos de alto contraste» en Accesibilidad → Visión, desactivado de serie. Los avisos de ataque enemigos (también los de jefes y la Sentencia) llevan un borde blanco fino y continuo con una sombra debajo (amarillo justo antes del golpe) y franjas diagonales tenues oscuro-claro. Mantienen el color del tipo y no tapan el escenario. Los textos nuevos del ajuste van en los 7 idiomas (`lang-en.js`, `lang-updates.js`).
- **Bola Voltio y Bola Neblina con forma propia** (`js/entities/vfx.js`): eran iguales que Impactrueno y casi iguales que Confusión. Ahora tienen pixel art nuevo de 4 fotogramas: esfera eléctrica con chispas cian que giran, y bruma psíquica en espiral con borde que respira.

## Antes y después

### Shiny en la Pokédex (móvil horizontal, 844×390)
| Antes: el selector es una raya y no se puede tocar | Después: se elige el shiny |
|---|---|
| <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/bugs-x/bug6-antes-dex-844x390.png" width="420"> | <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/bugs-x/bug6-despues-dex-844x390-shiny-elegido.png" width="420"> |

### Pokémon perdido y grietas
| Antes: se cansa de esperar durante la grieta | Después: al volver sigue a tu lado |
|---|---|
| <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/bugs-x/bug17-antes-3-se-ha-ido.png" width="420"> | <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/bugs-x/bug17-despues-4-al-volver.png" width="420"> |

### Niebla y Sentencia de Arceus (se ven igual y van más fluidas)
| Antes | Después |
|---|---|
| <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/bugs-x/bug20-antes-niebla.png" width="420"> | <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/bugs-x/bug20-despues-niebla.png" width="420"> |
| <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/bugs-x/bug20-antes-sentencia.png" width="420"> | <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/bugs-x/bug20-despues-sentencia.png" width="420"> |

Medidas: [FPS](https://github.com/kiev-amaterasu/pokesurvivor/blob/capturas/bugs-x/bug20-medidas.txt) · [sonido](https://github.com/kiev-amaterasu/pokesurvivor/blob/capturas/bugs-x/bug19-medidas.txt) · [cooperativo](https://github.com/kiev-amaterasu/pokesurvivor/blob/capturas/bugs-x/bug4-test.txt)

### Avisos de alto contraste
| Antes | Después (ajuste activado) |
|---|---|
| <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/bugs-x/bug25v3-antes-hierba.png" width="420"> | <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/bugs-x/bug25v3-despues-hierba.png" width="420"> |
| <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/bugs-x/bug25v3-antes-deuteranopia.png" width="420"> | <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/bugs-x/bug25v3-despues-deuteranopia.png" width="420"> |
| <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/bugs-x/bug25v3-antes-volcan.png" width="420"> | <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/bugs-x/bug25v3-despues-volcan.png" width="420"> |

La segunda fila simula deuteranopia (daltonismo rojo-verde) y la tercera es el volcán. El ajuste, en Accesibilidad:

<img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/bugs-x/bug25-despues-ajuste.png" width="560">

### Bola Voltio y Bola Neblina
| Antes | Después |
|---|---|
| <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/bugs-x/bug14-antes-comparativa.png" width="420"> | <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/bugs-x/bug14-despues-comparativa.png" width="420"> |

En partida:

| Bola Voltio | Bola Neblina |
|---|---|
| <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/bugs-x/bug14-despues-partida-bola-voltio.png" width="420"> | <img src="https://raw.githubusercontent.com/kiev-amaterasu/pokesurvivor/capturas/bugs-x/bug14-despues-partida-bola-neblina.png" width="420"> |

## Pruebas

- Pasan todos los tests (`node --test tests/*.test.cjs`) y `node tools/build.js` compila sin errores (`build_langs.js --faltan`: 0 en cada idioma).
- Cada arreglo probado en Chromium con Playwright, en modo local (sin tocar el Firebase de producción), con capturas de antes y después y medidas.
- El cooperativo (cambio de Pokémon) se probó con dos `G.Social` reales sobre una Realtime Database simulada.
- Falta probar en un móvil real el sonido y los FPS.

## Novedades propuestas

No lleva entrada en Novedades. Por si te sirve:

**Nuevo (`new`)**

- Accesibilidad: nuevo ajuste «Avisos de alto contraste» (Ajustes → Accesibilidad → Visión). Las zonas de ataque de los enemigos se ven con borde blanco y negro y rayadas, sin depender del color: pensado para el daltonismo. Viene desactivado.
  - _EN:_ Accessibility: new "High-contrast warnings" setting (Settings → Accessibility → Vision). Enemy attack zones get a black-and-white border and stripes, so you don't have to rely on color: made for color blindness. It is off by default.

**Arreglos (`fix`)**

- Bola Voltio y Bola Neblina tienen por fin su propio dibujo: una esfera eléctrica con chispas que giran y una bruma psíquica en espiral. Ya no se confunden con Impactrueno ni con Confusión.
  - _EN:_ Electro Ball and Mist Ball finally have their own look: an electric sphere with spinning sparks and a swirling psychic mist. They no longer get mixed up with Thunder Shock and Confusion.
- Móvil en horizontal: en la ficha de la Pokédex ya se puede elegir la versión shiny. El selector Normal/Shiny se quedaba aplastado en una raya y no se podía tocar.
  - _EN:_ Mobile in landscape: you can now pick the shiny version on the Pokédex page. The Normal/Shiny selector was squashed into a thin line and could not be tapped.
- Cooperativo: si cambias de Pokémon (o de normal a shiny) estando en una sala, tus compañeros ya te ven con el nuevo. Antes veían el anterior, aunque con tus ataques nuevos.
  - _EN:_ Co-op: if you change Pokémon (or switch between normal and shiny) while in a room, your teammates now see the new one. Before, they saw the previous one, though with your new attacks.
- Grietas: el Pokémon perdido que llevas a su marca ya no desaparece al entrar en una grieta. Te espera fuera y, al volver, sigue a tu lado.
  - _EN:_ Rifts: the lost Pokémon you are taking to its mark no longer disappears when you enter a rift. It waits outside and is right next to you when you come back.
- Móvil: el sonido ya no se satura en los combates con mucho jaleo. Sonaban más efectos a la vez de los que aguanta el móvil y se distorsionaban.
  - _EN:_ Mobile: sound no longer distorts in hectic fights. More effects played at once than the phone could handle, and they got distorted.
- Más fluido con niebla y en la Sentencia de Arceus: en algunos móviles bajaba mucho (hasta 10 fotogramas por segundo con niebla). Se ve igual que antes.
  - _EN:_ Smoother in fog and during Arceus's Judgment: on some phones it dropped a lot (down to 10 frames per second in fog). It looks the same as before.


---

Mismo formato que la de arreglos de issues: un commit sobre tu main, sólo código fuente, se puede fusionar con el botón.
