# 🐳 Docker Compose Sammlung (Lautfunk)

Eine Sammlung von `docker-compose` Konfigurationen für verschiedene Dienste (NAS, Server, Tools).

## 📂 Verfügbare Vorlagen

| Datei | Beschreibung |
|-------|--------------|
| **OpenClaw Ugreen NAS** | OpenClaw Agent Setup für Ugreen NAS (mit iGPU & Persistent-SSH) |
| **Pi-Hole Ungreen NAS** | Pi-Hole Setup (Adblocker) für NAS |
| **watchtower** | Automatisches Update von Docker Containern |

---

## 💡 Details & Wichtige Hinweise

### 🦞 OpenClaw Ugreen NAS
Diese Konfiguration ist speziell für Ugreen NAS Systeme angepasst.

**Besonderheiten:**
- **Build Context**: Nutzt `build: .` mit `dockerfile: Dockerfile`. Das bedeutet, diese Datei muss idealerweise **im Root des OpenClaw-Quellcode-Repos** ausgeführt werden (oder der Pfad angepasst werden).
- **iGPU Passthrough**: `/dev/dri:/dev/dri` ist aktiviert, damit Hardware-Beschleunigung (für Whisper/Medien) funktioniert.
- **Persistenz**: Neben dem Config-Ordner (`.openclaw`) werden auch:
  - `~/.local` (für installierte Tools wie Gemini CLI)
  - `~/.ssh` (für GitHub Keys)
  persistent gespeichert. Das verhindert, dass man sich nach jedem Neustart neu einloggen muss.

**Nutzung:**
1. Inhalt von `OpenClaw Ugreen NAS` kopieren.
2. Im OpenClaw-Ordner als `docker-compose.yml` speichern.
3. Ggf. Pfade bei `volumes:` anpassen (wenn dein NAS anders organisiert ist).
4. Starten: `docker compose up -d --build`

### 🛡 Pi-Hole
Standard-Setup für netzwerkweites Ad-Blocking.
Achte darauf, dass Port 53 auf dem NAS nicht kollidiert (oder nutze macvlan).

### 🔄 Watchtower
Überwacht laufende Container und aktualisiert sie automatisch, wenn neue Images verfügbar sind.

---
*Managed by OpenClaw*
