# MYGAME // C64 EDITION

Rundenbasiertes 2D-Artillery-Spiel (Worms-Klon) als einzelne `index.html`. C64-Farbpalette, Canvas-Rendering, kein Build-Step.

## Starten

Einfach `index.html` im Browser öffnen (Doppelklick oder Live Server).

## Architektur

Alles in einer Datei: `index.html` mit inline CSS und JS.

| Klasse | Aufgabe |
|---|---|
| `Terrain` | Heightmap-Generierung, Pixel-Kollision, Krater-Explosionen |
| `Worm` | Spielfigur, Physik, Ziellinie, HP |
| `Projectile` | Geschoss mit Bogen-Physik und Trail |
| `Particle` | Explosions-Partikel |
| `DamageText` | Schwebende Schadenszahlen |
| `GameEngine` | Game-Loop, Input, Zustandsmaschine, HUD |

## Game-States

`idle → playing → firing → exploding → waiting → playing → … → gameover`

## Steuerung

| Taste | Aktion |
|---|---|
| A / D | Wurm bewegen |
| W / S | Zielwinkel ändern |
| SPACE halten | Schussstärke aufladen |
| SPACE loslassen | Feuern |

## Palette (`C`-Objekt)

C64-Farben definiert in `const C = { ... }` am Anfang des Scripts. Farben dort zentral ändern, nicht inline im Draw-Code.

## Terrain-Rendering

`Terrain.draw()` regeneriert `imageData` nur wenn `dirty = true` (nach Explosion oder Init), ruft aber jedes Frame `putImageData` auf — so wird der Canvas als Hintergrund gecleart ohne alles neu zu berechnen.

## Bekannte Einschränkungen

- Kein Sound
- Nur Tastatursteuerung (kein Gamepad/Touch)
- KI fehlt — reines Hotseat-Multiplayer
