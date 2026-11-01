# Stutter — glitch effect for the Zoom MS-50G

**[Español](#español) · [English](#english)**

---

## Español

**Stutter** es un efecto de glitch para la Zoom MultiStomp **MS-50G**. Corta lo
que tocas en rebanadas y, al azar, reemplaza algunas por repeticiones,
ratchets, fragmentos al revés, frenadas de cinta o saltos de octava. Con
**Freeze** congela un fragmento en loop mientras sigues tocando encima.

Funciona con guitarra, bajo y sintetizadores.

> ⚠️ **Efecto no oficial.** No está hecho ni respaldado por Zoom. Instalar
> efectos de terceros puede colgar el pedal hasta que lo apagues y prendas.
> Respalda tu pedal antes de instalar (ver [Instalación](#instalación)).
> Lo usas bajo tu propio riesgo.

### Compatibilidad

| | |
|---|---|
| Probado en | Zoom MS-50G <!-- agrega aquí la versión de firmware --> |
| Debería funcionar en | MS-60B y MS-70CDR (mismo formato de efecto), sin probar todavía |
| Categoría en el pedal | SFX |
| Archivo | `Stutter.ZDL` |
| ID del efecto | `0x070001D6` (grupo 7, número 470) |
| Memoria | 512 KB (buffer estéreo de 1.49 s) |

### Cómo funciona

Stutter graba continuamente lo que entra. Un reloj interno divide el audio en
**rebanadas** del largo de *Size*. Al final de cada rebanada tira un dado: con
probabilidad *Chance*, la rebanada siguiente se reemplaza por una manipulación
del audio recién grabado:

| Glitch | Qué hace |
|---|---|
| **Repeat** | Repite el último fragmento. Con *Chaos* alto, en subdivisiones cada vez más cortas (ratchets) |
| **Reverse** | Toca el fragmento al revés |
| **Tape stop** | Frena el audio como una cinta que se detiene |
| **Octave up** | Repite el fragmento al doble de velocidad (+12 semitonos) |

Cuando no hay glitch, la señal pasa limpia. Todas las transiciones tienen
fundidos cortos, así que no hay clicks.

### Parámetros

El pedal muestra los parámetros en dos páginas de tres knobs.

**Página 1**

| Knob | Qué hace | Por defecto |
|---|---|---|
| **SIZE** | Largo de cada rebanada, de 30 a 700 ms | 35 (≈ 112 ms) |
| **CHANCE** | Probabilidad de que una rebanada se convierta en glitch. 0 = nunca, 100 = siempre | 50 |
| **CHAOS** | Variedad de los glitches. En 0 solo hay repeticiones; al subirlo aparecen subdivisiones, reversa, tape stop y octava arriba | 30 |

Valores de Size:

| Knob | 0 | 25 | 50 | 75 | 100 |
|---|---|---|---|---|---|
| Rebanada | 30 ms | 72 ms | 198 ms | 407 ms | 700 ms |

Qué agrega Chaos:

| Knob | Repeat | Cada uno de Reverse / Tape stop / Octave up | Subdivisión más corta |
|---|---|---|---|
| 0 | 100 % | 0 % | rebanada completa |
| 25 | 81 % | 6 % | rebanada completa |
| 50 | 62 % | 12 % | 1/2 |
| 75 | 44 % | 19 % | 1/4 |
| 100 | 25 % | 25 % | 1/8 |

**Página 2**

| Knob | Qué hace | Por defecto |
|---|---|---|
| **CRUSH** | Bitcrusher aplicado **solo al audio glitcheado**: baja la resolución (de 12 a 4 bits) y la frecuencia de muestreo (hasta ~2.8 kHz). La señal limpia no se toca | 0 |
| **MIX** | Cuánto reemplaza el glitch a la señal seca. 100 = el glitch reemplaza por completo; más abajo, se mezcla con lo que tocas | 100 |
| **FREEZE** | En 50 o más, retiene el fragmento actual en loop indefinido | 0 |

**Freeze en detalle**

- Si suena un Repeat, Reverse u Octave up, ese mismo fragmento queda en loop.
- Si no suena ningún glitch, captura la última rebanada (del largo de *Size*).
- Si está sonando un Tape stop, espera a que termine y luego captura.
- Mientras retiene no graba ni genera glitches nuevos, y puedes tocar encima en
  seco. *Crush* y *Mix* siguen funcionando sobre el loop.
- Al soltar, el loop termina su vuelta con un fundido. Los glitches vuelven
  cuando hay una rebanada completa de audio nuevo.

Freeze es un knob, no un footswitch: el footswitch de la MultiStomp solo prende
y apaga el efecto.

Mientras no muevas un knob, el efecto usa su valor por defecto. Desde que lo
mueves, vale lo que marca el pedal.

### Ideas de uso

- **Ratchets sobre un riff o un bajo secuenciado:** Size 20–35, Chance 60,
  Chaos 55–70, Mix 100.
- **Glitch ocasional y musical:** Size 40–60, Chance 20–30, Chaos 10, Mix 100.
- **Lo-fi roto:** Chance 80, Chaos 70, Crush 50–60.
- **Drone para tocar encima:** toca una nota o acorde con Chance en 0, sube
  Freeze y sigue tocando. Baja Mix para mezclar el loop con tu señal.

### Instalación

Necesitas un computador (Windows o macOS), el cable USB del pedal y
[Zoom Effect Manager](https://zoomeffectmanager.com/en/download/) **2.3.3 o
más nuevo** (versiones anteriores no leen efectos desde una carpeta).

**1. Respalda tu pedal.** Zoom Effect Manager puede eliminar del pedal los
efectos que no reconoce al escribir. Antes de instalar:

- Guarda tus patches. La app *MS50G Editor* (iPhone/iPad) los respalda y
  restaura; pide firmware v3.10.
- En Zoom Effect Manager, importa la lista de efectos del pedal y guárdala en
  un archivo. Saca también una captura de pantalla.
- Descarga de [zoomcorp.com](https://zoomcorp.com) el firmware oficial de la
  MS-50G y el *MS-50G Effect Manager* oficial. Son tu plan para volver a
  fábrica si algo sale mal.

**2. Descarga** `Stutter.ZDL` desde [Releases](../../releases) y guárdalo en
una carpeta propia (por ejemplo, `ZoomCustom/`).

**3. Instala:**

1. Conecta el pedal por USB y **después** abre Zoom Effect Manager.
2. Abre *Settings* y elige *Read Effects from folder*. Selecciona la carpeta
   donde guardaste `Stutter.ZDL`.
3. En el filtro de fuentes, activa *Effects from devices* y *From Folder*.
4. Agrega **Stutter** a la lista de efectos y escribe al pedal.

**4. Úsalo:** en el pedal, elige un efecto de la categoría **SFX** y busca
Stutter.

> **Deja instalado al menos un efecto de fábrica de la categoría SFX.** Un
> efecto custom puede quedar invisible en el pedal si es el único de su
> categoría.

**Desinstalar:** quítalo de la lista en Zoom Effect Manager y vuelve a
escribir al pedal.

### Problemas comunes

| Síntoma | Qué hacer |
|---|---|
| Stutter no aparece en el pedal | Verifica que haya otro efecto SFX de fábrica instalado |
| Zoom Effect Manager muestra `repeating index effect - 0x070001D6` | Otro efecto usa el mismo ID. **No escribas al pedal.** Quita uno de los dos de la carpeta y del pedal |
| Pitido intermitente (~690 Hz) con el efecto encendido | El pedal le dio menos memoria de la que necesita (512 KB). El efecto deja pasar la señal limpia y avisa con el pitido. Abre un issue con tu modelo y firmware |
| El pedal se cuelga | Apágalo y préndelo. Si la lista de efectos queda mal, reinstala el firmware oficial |

Para reportar un problema, abre un [issue](../../issues) con el modelo del
pedal, la versión de firmware, la posición del efecto en la cadena y qué
estabas haciendo.

### Créditos

Desarrollado por Wladi. El DSP se diseñó y probó en el computador antes de
llevarlo al pedal, y se compiló con el toolchain
[repeat98/ZoomMultistompZDL](https://github.com/repeat98/ZoomMultistompZDL)
(MIT), que hace posible cargar efectos propios en las MultiStomp sin el SDK de
Zoom.

Zoom, MultiStomp y MS-50G son marcas de Zoom Corporation. Este proyecto no
está afiliado a Zoom.

### Licencia

MIT. Ver [LICENSE](LICENSE).

---

## English

**Stutter** is a glitch effect for the Zoom **MS-50G** MultiStomp. It slices
what you play and randomly replaces some slices with repeats, ratchets,
reversed fragments, tape stops or octave jumps. **Freeze** holds a fragment in
a loop while you keep playing over it.

It works with guitar, bass and synths.

> ⚠️ **Unofficial effect.** It is not made or endorsed by Zoom. Installing
> third-party effects can freeze the pedal until you power-cycle it. Back up
> your pedal before installing (see [Installation](#installation)). Use at
> your own risk.

### Compatibility

| | |
|---|---|
| Tested on | Zoom MS-50G <!-- add the firmware version here --> |
| Should work on | MS-60B and MS-70CDR (same effect format), not tested yet |
| Category on the pedal | SFX |
| File | `Stutter.ZDL` |
| Effect ID | `0x070001D6` (group 7, number 470) |
| Memory | 512 KB (1.49 s stereo buffer) |

### How it works

Stutter records its input continuously. An internal clock divides the audio
into **slices** of length *Size*. At the end of each slice it rolls a die:
with probability *Chance*, the next slice is replaced with a manipulation of
the audio just recorded:

| Glitch | What it does |
|---|---|
| **Repeat** | Repeats the last fragment. With high *Chaos*, in shorter and shorter subdivisions (ratchets) |
| **Reverse** | Plays the fragment backwards |
| **Tape stop** | Slows the audio down like a stopping tape |
| **Octave up** | Repeats the fragment at double speed (+12 semitones) |

When there is no glitch, the signal passes through clean. Every transition
has a short fade, so there are no clicks.

### Parameters

The pedal shows the parameters on two pages of three knobs.

**Page 1**

| Knob | What it does | Default |
|---|---|---|
| **SIZE** | Slice length, from 30 to 700 ms | 35 (≈ 112 ms) |
| **CHANCE** | Probability that a slice becomes a glitch. 0 = never, 100 = always | 50 |
| **CHAOS** | Glitch variety. At 0 there are only repeats; turning it up adds subdivisions, reverse, tape stop and octave up | 30 |

Size values:

| Knob | 0 | 25 | 50 | 75 | 100 |
|---|---|---|---|---|---|
| Slice | 30 ms | 72 ms | 198 ms | 407 ms | 700 ms |

What Chaos adds:

| Knob | Repeat | Each of Reverse / Tape stop / Octave up | Shortest subdivision |
|---|---|---|---|
| 0 | 100 % | 0 % | full slice |
| 25 | 81 % | 6 % | full slice |
| 50 | 62 % | 12 % | 1/2 |
| 75 | 44 % | 19 % | 1/4 |
| 100 | 25 % | 25 % | 1/8 |

**Page 2**

| Knob | What it does | Default |
|---|---|---|
| **CRUSH** | Bitcrusher applied **only to the glitched audio**: lowers the resolution (from 12 to 4 bits) and the sample rate (down to ~2.8 kHz). The clean signal is untouched | 0 |
| **MIX** | How much the glitch replaces the dry signal. 100 = the glitch fully replaces it; lower values blend it with what you play | 100 |
| **FREEZE** | At 50 or above, holds the current fragment in an endless loop | 0 |

**Freeze in detail**

- If a Repeat, Reverse or Octave up is playing, that fragment keeps looping.
- If no glitch is playing, it captures the last slice (of length *Size*).
- If a Tape stop is playing, it waits for it to finish and then captures.
- While holding, it neither records nor creates new glitches, and you can play
  dry over the loop. *Crush* and *Mix* still act on the loop.
- On release, the loop finishes its cycle with a fade. Glitches come back once
  a full slice of new audio has been recorded.

Freeze is a knob, not a footswitch: the MultiStomp footswitch only turns the
effect on and off.

Until you turn a knob, the effect uses its default value. Once you turn it,
the value shown on the pedal applies.

### Ideas

- **Ratchets on a riff or a sequenced bass line:** Size 20–35, Chance 60,
  Chaos 55–70, Mix 100.
- **Occasional, musical glitches:** Size 40–60, Chance 20–30, Chaos 10,
  Mix 100.
- **Broken lo-fi:** Chance 80, Chaos 70, Crush 50–60.
- **Drone to play over:** play a note or chord with Chance at 0, turn Freeze
  up and keep playing. Lower Mix to blend the loop with your signal.

### Installation

You need a computer (Windows or macOS), the pedal's USB cable and
[Zoom Effect Manager](https://zoomeffectmanager.com/en/download/) **2.3.3 or
newer** (earlier versions cannot read effects from a folder).

**1. Back up your pedal.** When writing, Zoom Effect Manager can remove
effects it does not recognize from the pedal. Before installing:

- Save your patches. The *MS50G Editor* app (iPhone/iPad) backs them up and
  restores them; it requires firmware v3.10.
- In Zoom Effect Manager, import the effect list from the pedal and save it
  to a file. Take a screenshot as well.
- Download the official MS-50G firmware and the official *MS-50G Effect
  Manager* from [zoomcorp.com](https://zoomcorp.com). They are your way back
  to factory settings if something goes wrong.

**2. Download** `Stutter.ZDL` from [Releases](../../releases) and save it in
a folder of its own (for example, `ZoomCustom/`).

**3. Install:**

1. Connect the pedal over USB **first**, then open Zoom Effect Manager.
2. Open *Settings* and choose *Read Effects from folder*. Select the folder
   where you saved `Stutter.ZDL`.
3. In the source filter, enable *Effects from devices* and *From Folder*.
4. Add **Stutter** to the effect list and write it to the pedal.

**4. Use it:** on the pedal, choose an effect from the **SFX** category and
browse to Stutter.

> **Keep at least one factory SFX effect installed.** A custom effect can be
> invisible on the pedal if it is the only one in its category.

**Uninstall:** remove it from the list in Zoom Effect Manager and write to
the pedal again.

### Troubleshooting

| Symptom | What to do |
|---|---|
| Stutter does not show up on the pedal | Check that another factory SFX effect is installed |
| Zoom Effect Manager reports `repeating index effect - 0x070001D6` | Another effect uses the same ID. **Do not write to the pedal.** Remove one of the two from the folder and from the pedal |
| Intermittent beep (~690 Hz) while the effect is on | The pedal gave it less memory than it needs (512 KB). The effect passes the clean signal and beeps as a warning. Open an issue with your model and firmware |
| The pedal freezes | Power-cycle it. If the effect list ends up wrong, reinstall the official firmware |

To report a problem, open an [issue](../../issues) with the pedal model, the
firmware version, the effect's position in the chain and what you were doing.

### Credits

Developed by Wladi. The DSP was designed and tested on a computer before going
to the pedal, and compiled with the
[repeat98/ZoomMultistompZDL](https://github.com/repeat98/ZoomMultistompZDL)
toolchain (MIT), which makes it possible to load custom effects on the
MultiStomp pedals without Zoom's SDK.

Zoom, MultiStomp and MS-50G are trademarks of Zoom Corporation. This project
is not affiliated with Zoom.

### License

MIT. See [LICENSE](LICENSE).
