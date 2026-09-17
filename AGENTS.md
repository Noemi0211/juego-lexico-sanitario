# AGENTS.md

Notas de trabajo para agentes de IA que colaboren en este repositorio.

## Proyecto

Aplicación web estática de un juego de parejas para trabajar el léxico sanitario (prefijos y sufijos). Todo el código vive en `index.html` (HTML + CSS + JavaScript vanilla, sin dependencias ni build).

- Niveles: Fácil (6 parejas), Medio (12 parejas), Difícil (24 parejas).
- Layout del tablero: montículo piramidal estilo Mahjong, con patrón de filas por nivel.

## Despliegue

- Repositorio: https://github.com/Noemi0211/juego-lexico-sanitario
- Deploy: GitHub Pages desde la rama `master` -> https://noemi0211.github.io/juego-lexico-sanitario/
- Al hacer `git push` a `master`, GitHub Pages reconstruye el sitio automáticamente.

## Cómo probar

- Escritorio: abrir `index.html` en el navegador.
- Móvil: recargar forzando caché o en pestaña privada sobre la URL de GitHub Pages.

---

## Backlog: mejoras de experiencia en móvil

Marcar con `[x]` al completar. Cada tarea incluye una pista de implementación.

### Bloque crítico

- [x] **1. Añadir `<meta name="viewport">`**
  `width=device-width, initial-scale=1`. Sin él, los móviles renderizan a ~980 px y encogen la página, por eso se veía pequeño.
- [x] **2. Tamaño de fuente de las cartas acorde al tamaño real de la carta**
  El `clamp(..., 1.1vw, ...)` nunca crecía en móvil (`1.1vw` ≈ 4 px). Se calcula `--fuente` en JS según `anchoCarta` y se aplica en `.carta .cara`.
- [x] **3. Evitar que se recorten palabras largas**
  `.carta` tiene `overflow: hidden` y `.cara` no partía palabras ("inflamación", "agrandamiento"...). Añadir `overflow-wrap`/`hyphens` y `lang="es"` en `<html>`.

### Feedback táctil

- [ ] **4. Desactivar hover "pegajoso" en pantalla táctil**
  Envolver `.carta:not(.girada):hover` en `@media (hover: hover)` y añadir un estado `:active` con feedback visual.
- [ ] **5. `touch-action: manipulation` en cartas y botones**
  Elimina el retardo de 300 ms del doble toque y evita el zoom accidental.
- [ ] **6. Vibración al acertar/fallar (Android)**
  `navigator.vibrate([...])` con comprobación de soporte; en iOS no está disponible.

### Pulido

- [ ] **7. Animación al emparejar**
  Ahora las cartas emparejadas desaparecen de golpe (solo `visibility: hidden`). Añadir transición de `opacity` + `transform: scale` antes de ocultarlas.
- [ ] **8. `overscroll-behavior: contain` en el tablero**
  Evitar que el scroll del tablero arrastre la página completa (efecto rebote en móvil).
- [ ] **9. Inicializar el audio al pulsar "Jugar"**
  En iOS el primer sonido puede perderse porque el `AudioContext` se crea en el primer `girar`. Crearlo/reanudarlo en el botón de inicio.

---

## Convenciones

- No añadir comentarios innecesarios al código.
- Mantener el estilo existente (JavaScript vanilla, nombres de variables en español).
- Probar los tres niveles (Fácil/Medio/Difícil) antes de dar una tarea por completada.
