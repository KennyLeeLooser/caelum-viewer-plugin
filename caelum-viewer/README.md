# Caelum 3D-Viewer – Plugin für Claude Code und Codex

Der Caelum 3D-Viewer lässt Claude Code und Codex 3D-Dateien ansehen und ausgeben – lokal auf deinem Windows-PC.
Dieses Repo ist ein Plugin-Marktplatz (`caelum-viewer`) mit dem Plugin `caelum-viewer`.

- **Formate:** GLB, glTF, OBJ, STL, 3MF, DXF direkt; FBX, USDZ und BLEND über ein installiertes [Blender](https://www.blender.org/).
- **Ausgabe:** PNG, JPG, PDF-Datenblatt mit Maßen, GIF als 360°-Drehung, Kamerafahrt oder Animation – ohne Abschneiden.
- **Vorschau:** Claude bekommt ein Bild zurück und sieht das Modell selbst; `show_model` zeigt es als echte 3D-Ansicht im Chat (drehen, zoomen, Animation, GIF).

**Ohne Installation (ChatGPT und claude.ai im Browser):** Connector bzw. eigenen MCP-Server mit der Adresse `https://api.caelum.one/viewer/mcp` hinzufügen (keine Anmeldung). Modelle kommen dort als öffentliche https-Adresse oder Upload; Dateien auf dem eigenen PC gehen nur mit diesem Plugin.

## 1. Voraussetzungen
- Windows 10/11 (x64)
- Sonst nichts: `CaelumViewer.exe` bringt alles mit (keine .NET-Installation nötig). Blender nur für FBX, USDZ und BLEND.

## 2. Installieren

### Claude Code
```
/plugin marketplace add KennyLeeLooser/caelum-viewer-plugin
```
```
/plugin install caelum-viewer@caelum-viewer
```

### Codex
```
codex plugin marketplace add KennyLeeLooser/caelum-viewer-plugin
```
Danach in Codex unter **Plugins** „Caelum 3D-Viewer“ installieren (oder `codex plugin add caelum-viewer@caelum-viewer`).

Hast du den MCP-Server `caelum-viewer` schon von Hand eingetragen, entferne diesen Eintrag, sonst gibt es ihn doppelt
(`claude mcp remove caelum-viewer -s user` bzw. `codex mcp remove caelum-viewer`).

## 3. Was das Plugin mitbringt
| Teil | Claude Code | Codex |
|---|---|---|
| MCP-Server `caelum-viewer`: `find_models`, `model_info`, `preview`, `render`, `make_gif`, `render_folder`, `list_presets`, `open_in_viewer`, `show_model` | ✓ | ✓ |
| Skill `caelum-viewer` (wann und wie die Werkzeuge helfen) | ✓ | ✓ |
| Befehle `/caelum-viewer:ansehen`, `:gif`, `:datenblatt` | ✓ | – |

Beispiele: „Zeig mir `C:\Modelle\stuhl.glb` von vorne.“ · „Mach ein 480 px Dreh-GIF davon auf #1F1E1D.“ ·
„Gib ein Datenblatt mit Maßen als PDF aus.“

Ausgaben landen standardmäßig in `Dokumente\Caelum Viewer\<Modell>`.

## 4. Sicherheit und Datenschutz
- Alles läuft lokal. Das Plugin startet `CaelumViewer.exe mcp` über stdio; es öffnet keinen Netzwerkanschluss und sendet nichts ins Internet.
- Gelesen werden nur die Dateien, die du (oder Claude in deinem Auftrag) nennst; geschrieben wird nur in den Ausgabeordner.
- Einstellungen und gespeicherte Ansichten liegen in `%APPDATA%\CaelumViewer`.

## 5. Ohne Plugin (nur MCP-Server)
Claude Code: `claude mcp add caelum-viewer -- "C:\Pfad\zu\caelum-viewer\server\CaelumViewer.exe" mcp`

Codex, `~/.codex/config.toml`:
```toml
[mcp_servers.caelum-viewer]
command = "C:\Pfad\zu\caelum-viewer\server\CaelumViewer.exe"
args = ["mcp"]
```
Die Exe ist auch ein normales Fenster-Programm: Doppelklick öffnet den Viewer.

## Lizenz
Freeware: kostenlos nutzen und unverändert weitergeben; kein Verkauf, keine Änderungen. Details in [LICENSE](LICENSE),
Drittanbieter in [THIRD-PARTY-NOTICES.md](THIRD-PARTY-NOTICES.md).
© 2026 Caelum GmbH, Kenny Looser.
