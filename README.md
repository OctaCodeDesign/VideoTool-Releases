# VideoTool

Eigenständiges Windows-Programm für KI-Videos mit **MiniMax H3** – ohne ComfyUI.
Long Takes, Musikvideos mit exaktem Lipsync, Song-Analyse, Bilder, YouTube-Upload – und steuerbar durch KI-Agenten (MCP).

**Download:** neueste Version unter [Releases](https://github.com/OctaCodeDesign/VideoTool-Releases/releases/latest) → `VideoTool-Setup-<Version>.exe`

---

## Voraussetzungen

| | Minimum | Empfohlen |
|---|---|---|
| Grafikkarte | NVIDIA RTX 30xx/40xx/50xx mit 12 GB | 24–32 GB (RTX 4090, 5090) |
| Treiber | 560 | 580 oder neuer (Pflicht für RTX 50xx) |
| Arbeitsspeicher | 32 GB | 64 GB oder mehr |
| Festplatte | ~45 GB | ~115 GB (alle Modelle), SSD/NVMe |
| System | Windows 10/11, 64 Bit | |

Keine Administratorrechte nötig. Python, PyTorch und ffmpeg bringt das Setup selbst mit – nichts wird systemweit verändert.

## Installation

1. `VideoTool-Setup-<Version>.exe` starten. Ist eine neuere Version veröffentlicht, bietet das Setup sie an.
2. **Lizenzen** der KI-Modelle bestätigen.
3. **Installationsordner** und **Modellordner** wählen (Modelle: bis zu 100 GB – am besten eine SSD).
4. **Bausteine** wählen. Das Setup liest Grafik- und Arbeitsspeicher aus und zeigt bei jedem Modell
   „optimal“, „läuft, aber langsamer“ oder „nicht lauffähig“ (ausgegraut):
   - Grundpaket (Pflicht): Text-Encoder, VAEs, Upscaler, LoRAs – 22 GB
   - Videomodell **kompakt** (21 GB) und/oder **groß** (34 GB, Original-Long-Take-Qualität)
   - Song-Analyse (4,5 GB) · Qwen Image (17 GB, nur nicht-kommerziell)
5. **Vorhandene Modelle:** Das Setup durchsucht schon beim Start alle Festplatten nach passenden Modellen
   (z. B. aus ComfyUI). Gefundene werden direkt dort verwendet – kein Download. Angezeigt wird, was noch
   geladen werden muss („Herunterzuladen: N Dateien, X GB“).
6. Optional einen **Hugging-Face-Token** eintragen (schnellere Downloads, wird nicht gespeichert).
7. Installieren – ein Fenster richtet Python, Pakete, ffmpeg und die Modelle ein (je nach Internet 1–3 Stunden).

Abgebrochen? Setup erneut starten oder im Startmenü **„Modelle reparieren“** – Fertiges wird übersprungen.

## Updates

VideoTool prüft beim Start auf neue Versionen und zeigt oben rechts **„⬆ Update verfügbar“**.
Unter **Einstellungen → Version & Updates**:
- **Kanal:** *Stabil* (Standard) oder *Beta* (auch Vorabversionen)
- **Versionsliste:** jede Version installierbar – auch eine ältere („Zurück auf diese“)

Einstellungen, Modelle und Videos bleiben bei Updates erhalten; neu benötigte Modelle werden nachgeladen.

## Bedienung in Kürze

- **Long Take:** nahtlose lange Einstellung aus Segmenten. Pro Segment Prompt, eigene Bilder, Kamera und Ton.
  `@` im Prompt zeigt alle Referenzen (`<Picture 1>` …). Timeline unten, Live-Vorschau in der Mitte.
- **Song-Analyse:** Song oder eigene Stems (z. B. Suno-Export) + Songtext → Sänger, Wörter, Beats, Clips;
  „Ins Projekt übernehmen“ legt pro Clip ein Long-Take-Segment mit Lipsync an.
- **Musikvideo, Einzelclip, Bilder, Assistent, YouTube** – jeweils eigener Bereich oben.
- **Hilfe** (Fragezeichen oben rechts): alle Anleitungen direkt im Programm.

## KI-Agenten (MCP)

VideoTool bringt einen **MCP-Server** mit (19 Werkzeuge: Clips/Long Takes rechnen, Songs analysieren,
Bilder erzeugen, Aufträge verfolgen …). VideoTool muss dabei laufen.
In der App unter **Hilfe → MCP / Agenten** stehen die Befehle mit dem Pfad deiner Installation zum Kopieren.

**Claude Code:**
```bash
claude mcp add videotool -- "<Installationsordner>\.venv\Scripts\videotool-mcp.exe"
```

**Claude Desktop** – `%APPDATA%\Claude\claude_desktop_config.json`, unter `mcpServers` ergänzen, dann Claude Desktop neu starten:
```json
{
  "mcpServers": {
    "videotool": { "command": "<Installationsordner>\.venv\Scripts\videotool-mcp.exe" }
  }
}
```

## Lizenzen der Modelle

VideoTool enthält keine KI-Modelle; das Setup lädt sie von ihren Original-Quellen auf Hugging Face.
MiniMax H3 steht unter der *MiniMax H3 Community License*, Qwen Image 2.1 unter der *Qwen Research License*
(nur nicht-kommerziell). Details: `LIZENZEN.txt` im Programmordner bzw. im Setup.
