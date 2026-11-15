---
name: caelum-viewer
description: Look at and export 3D files with the Caelum 3D-Viewer MCP tools (server "caelum-viewer") – GLB, glTF, OBJ, STL, 3MF, DXF directly; FBX, USDZ, BLEND via Blender. Use when the user wants to see a 3D model, asks what is in a 3D file, or wants PNG/JPG images, a PDF data sheet with dimensions, a 360° or animation GIF, or images for a whole folder of models.
---

# Caelum 3D-Viewer

Der Viewer rendert lokal (Software-Renderer, kein Fenster nötig). Ausgaben landen standardmäßig in
`Dokumente\Caelum Viewer\<Modell>`, sonst in `out_dir`.

## Werkzeuge (MCP-Server `caelum-viewer`)
- `model_info(path)` – Format, Dreiecke, Teile, Maße in m, Animationen, gespeicherte Stopps.
- `preview(path, view?)` – liefert ein Bild zurück: so siehst du das Modell selbst. Ansichten: Vorne, Hinten, Links,
  Rechts, Oben, Unten, Iso oder eigene Gieren/Nicken-Winkel.
- `render(path, formats=[png|jpg|pdf|gif], preset?, views?)` – alle Stopps ausgeben; PDF-Datenblatt mit Maßseite, Kopfzeile,
  Logo und Notiz je Stopp.
- `make_gif(path, mode, …)` – GIF ohne Abschneiden: `drehung` (360°), `stopps` (Kamerafahrt) oder `stand`
  (feste Kamera, zusammen mit `animation`). Farbe `#RRGGBB`, `gif_width`, `frames`, `delay_ms`.
- `render_folder(folder, formats?, …)` – alle Modelle eines Ordners mit denselben Blickrichtungen.
- `list_presets()` – Standardsätze (Standard, GIF-Rundgang, GIF-Präsentation, GIF-Drehung 360°, Technisch, eigener Satz).
- `open_in_viewer(path)` – Datei im Viewer-Fenster öffnen (nur wenn der Nutzer das Fenster will).
- `show_model(path)` – Vorschau mit Widget (für Hosts mit MCP-Apps-Unterstützung).

## Vorgehen
1. Erst `model_info` oder `preview`, damit du weißt, was im Modell steckt (Größe, Ausrichtung, Animationen).
2. Dann `render` oder `make_gif` mit den Wünschen des Nutzers. Steht ein Modell auf dem Kopf oder liegt,
   im Ergebnis darauf hinweisen (CAD-Dateien sind oft Z-oben).
3. Dem Nutzer die Pfade der erzeugten Dateien nennen; Bilder bei Bedarf mit `preview` selbst prüfen.

## Regeln
- Nur Dateien öffnen, die der Nutzer nennt oder die im Projekt liegen; nichts löschen oder überschreiben,
  was nicht vom Viewer stammt.
- FBX, USDZ und BLEND brauchen ein installiertes Blender (sonst klare Meldung weitergeben). STEP wird nicht
  unterstützt: vorher in Blender, Fusion oder Bambu Studio nach STL, 3MF oder GLB exportieren.
- Große Modelle (Millionen Dreiecke) brauchen einige Sekunden; GIFs klein halten (z. B. 480 px), wenn nichts anderes verlangt ist.
