# Thin-Client-Retro-AIO
Thin Client "Retro-AIO": Wiederbelebung eines alten Lenovo F0B3 All-in-One PCs als Media- und Retro-Gaming-Client (PS1/Game Boy) über Lubuntu. Backend-Streaming-Fähigkeit via Homeserver (Xeon E5-2697v2, 256GB RAM, AMD RX480) zur Latenzkompensation und zentralen Datenhaltung.

# Thin-Client Projekt

**Von Dennis Nolden**

---

## 📝 Projektdokumentation: Thin Client für Retro-Gaming und Media-Wiedergabe

### 1. 🎯 Projektziele und Anforderungen

#### Executive Summary (Einleitung)

In diesem Projekt ist es mein Ziel, einen **Thin Client** zu erstellen aus bestehender alter Hardware (Lenovo F0B3 AIO PC), um in meinem Wohnzimmer **Retrogaming** und **Medienwiedergabe** (wie über YouTube) über einen Beamer zu ermöglichen. [cite_start]Die Anbindung erfolgt drahtlos an den zentralen Homeserver. [cite: 34, 35]

| # | Ziel/Anforderung | Beschreibung |
| :--- | :--- | :--- |
| **P1** | Thin Client Funktion | Aufbau eines Thin Clients |
| **A1** | Hardware-Basis | Verwendung eines alten All-in-One (AIO) PCs (Lenovo F0B3) |
| **A2** | Bildausgabe | Bilddarstellung via Beamer |
| **A3** | Media-Wiedergabe | Wiedergabe von YouTube-Inhalten |
| **A4** | Retro-Gaming | Möglichkeit zum Spielen von Retro-Games |
| **A5** | Konnektivität | Verbindung zum Homeserver über WLAN |
| **A6** | Internetzugang | [cite_start]Vorhanden | [cite: 36]

---

### 2. 🖥️ Hardware-Basis und Infrastruktur

#### 2.1. Thin Client (AIO PC) – Frontend

| Komponente | Spezifikation | Rolle im Projekt |
| :--- | :--- | :--- |
| **Modell** | Lenovo F0B3 (AIO PC) | Frontend, lokaler Emulator-Host, Display-Ausgabe |
| **RAM** | 4 GB | Limitierende Ressource für anspruchsvolle Anwendungen |
| **Speicher** | 500 GB HDD-Festplatte | [cite_start]Lokaler Speicher für OS und Retro-Emulatoren/ROMs | [cite: 39]

#### 2.2. Homeserver (Backend)

| Komponente | Spezifikation | Rolle im Projekt |
| :--- | :--- | :--- |
| **CPU** | Intel(R) Xeon(R) CPU E5-2697 v2 @ 2.70GHz (12 Kerne) | Host für Virtualisierung, Game-Streaming-Server, Datenserver |
| **RAM** | 256 GB | Stellt ausreichend RAM für VMs, Container und Caching bereit |
| **GPU** | AMD RX480 | [cite_start]Dedizierte Grafikleistung für Transkodierung und/oder Gaming-Backend | [cite: 41]

---

### 3. 💻 Betriebssystem (OS) und Architekturentscheidung

#### 3.1. OS-Auswahl und Begründung (Thin Client)

| Option | Fokus | OS-Empfehlung | Begründung |
| :--- | :--- | :--- | :--- |
| **Fokus Allround** (Empfohlen) | YouTube & Thin Client | Lubuntu (LXQt) oder Xubuntu (XFCE) | Bieten eine optimale Balance aus Ressourcenverbrauch und Funktionalität (Webbrowser für YouTube, vollwertige Linux-Umgebung). [cite_start]| [cite: 44]

#### 3.2. Implementierung der Kernfunktionen

| Funktion | Software/Implementierung | Details |
| :--- | :--- | :--- |
| **YouTube (A3)** | Aktueller Webbrowser | Wiedergabe hängt von der CPU/GPU des Lenovo AIO ab. |
| **Retro-Gaming (A4)** | RetroArch Emulator | All-in-One-Lösung für Konsolen (NES, SNES, PS1, etc.) auf dem AIO. |
| **Homeserver-Zugriff (A5)** | Remmina (Remote Desktop) | Tools für RDP, VNC, SSH (Administration), etc. auf Linux verfügbar. |
| **Dateizugriff** | Samba/NFS | Integration von Samba (Windows) oder NFS (Linux) Freigaben. |
| **Konnektivität** | WLAN (Wi-Fi) | Standardmäßig unterstützt von den genannten Linux-Systemen. [cite_start]| [cite: 46]

---

### 4. 🚀 Rolle des Homeservers und Backend-Leistung

[cite_start]Der Homeserver dient als leistungsstarkes Backend, das die Schwächen des ressourcenlimitierten Thin Clients (4 GB RAM, schwächere lokale GPU) ausgleichen kann. [cite: 48]

| Einsatzszenario | Server-Komponente | Details zur Nutzung |
| :--- | :--- | :--- |
| **Erweiterte Emulation/Gaming** | Xeon CPU, 256 GB RAM | Hostet eine **Virtual Machine (VM)** oder Container, die per **Remote Desktop** (z.B. VNC oder Parsec) an den Thin Client gestreamt wird. |
| **Hardware-beschleunigtes Streaming** | AMD RX480 GPU | Ermöglicht GPU-Passthrough in eine Gaming-VM oder wird für die **Medien-Transkodierung** (z.B. Plex Media Server) verwendet. |
| **Zentrale Datenhaltung** | 256 GB RAM, HDD | Zentrale Speicherung aller Retro-ROMs und Media-Dateien. [cite_start]| [cite: 49]

---

### 5. ⚠️ Risikobewertung (Hardware)

* [cite_start]**Leistungsgrenze (A3):** Die lokale Wiedergabe von HD- oder 4K-YouTube-Videos auf dem Thin Client (**Lenovo F0B3**) könnte aufgrund der älteren AIO-Hardware (CPU/GPU) an ihre Grenzen stoßen. [cite: 51]
    * [cite_start]**Lösung:** Nutzung des Homeservers für das Rendering und Streaming zum Client (z.B. via Parsec), um die Last auf die **AMD RX480** zu verlagern. [cite: 52]
* [cite_start]**WLAN-Latenz (A5, A4):** Die WLAN-Verbindung ist der kritische Pfad für Gaming-Streaming oder schnelle Remote-Desktop-Sitzungen. [cite: 53]
    * [cite_start]**Lösung:** Empfehlung, ein 5-GHz-Netzwerk (falls möglich) zu nutzen oder, für kritische Anwendungen, eine temporäre LAN-Verbindung in Betracht zu ziehen. [cite: 54]

---
---

## 📝 Umsetzungsanleitung: Thin Client für Retro-Gaming & Media-Wiedergabe

### Phase I: Vorbereitung und Installation des Thin Client OS

[cite_start]**Ziel:** Installation des schlanken Betriebssystems Lubuntu auf dem Lenovo F0B3 AIO PC. [cite: 57]

#### I.1. Systemanforderungen und Medienvorbereitung

* [cite_start]**Thin Client Hardware:** Lenovo F0B3 AIO PC (4 GB RAM, 500 GB HDD). [cite: 59]
* [cite_start]**OS-Wahl:** Lubuntu (aktuellste LTS-Version wird empfohlen). [cite: 60]
* [cite_start]**Installationsmedium:** USB-Stick (min. 8 GB) zur Erstellung eines bootfähigen Live-Systems. [cite: 61]
* **Vorgehen:**
    1.  [cite_start]Lubuntu ISO-Datei von der offiziellen Website herunterladen. [cite: 63]
    2.  [cite_start]Bootfähigen USB-Stick mit einem Tool wie Rufus oder Balena Etcher erstellen. [cite: 64]

#### I.2. Installation von Lubuntu

1.  **Booten:** AIO PC mit dem vorbereiteten USB-Stick starten. [cite_start]Ggf. im BIOS/UEFI die Bootreihenfolge anpassen. [cite: 66]
2.  [cite_start]**Live-System:** Im GRUB-Menü die Option "Try or Install Lubuntu" wählen. [cite: 67]
3.  [cite_start]**Installationsstart:** Auf dem Desktop auf das Icon "Install Lubuntu" klicken. [cite: 68]
4.  [cite_start]**Basiskonfiguration:** Sprache, Zeitzone und Tastaturlayout auf Deutsch festlegen. [cite: 69]
5.  **Partitionierung (Wichtig):**
    * [cite_start]Die Option **"Festplatte löschen und Lubuntu installieren"** wählen, da die alte Hardware als reiner Thin Client genutzt werden soll. [cite: 71]
    * *Alternativ (für Experten):* Manuelle Partitionierung, falls eine separate `/home` Partition gewünscht wird. Lubuntu benötigt ca. [cite_start]8,5 GB freien Speicher. [cite: 72]
6.  [cite_start]**Benutzer anlegen:** Ersten Benutzer (mit Root-Rechten) und Passwort festlegen. [cite: 73]
7.  [cite_start]**Installation abschließen:** Nach Abschluss der Installation den PC neu starten und den USB-Stick entfernen. [cite: 74]

#### I.3. WLAN-Einrichtung (A5)

1.  [cite_start]Nach dem ersten Start auf dem Lubuntu-Desktop das **Netzwerk-Icon** in der Taskleiste (Panel) suchen. [cite: 76]
2.  [cite_start]Das gewünschte WLAN-Netzwerk (SSID) auswählen und das Passwort eingeben. [cite: 77]
3.  **Troubleshooting:** Sollte der WLAN-Adapter nicht erkannt werden:
    * [cite_start]Den AIO PC temporär per LAN-Kabel verbinden. [cite: 79]
    * [cite_start]Über das Terminal oder die **"Zusätzliche Treiber"**-Anwendung nach proprietären WLAN-Treibern suchen und diese installieren. [cite: 80]

---

### Phase II: Thin Client Funktionalität und Remoteverbindung

[cite_start]**Ziel:** Sicherstellung der Remote-Konnektivität zum Homeserver (Backend) zur Nutzung der Xeon/256GB/RX480-Ressourcen. [cite: 82]

#### II.1. Installation des Remote Desktop Clients (Remmina)

[cite_start]Der Remmina Remote Desktop Client wird für RDP/VNC/SSH-Verbindungen empfohlen. [cite: 84]

1.  [cite_start]Terminal öffnen (`Strg + Alt + T`). [cite: 85]
2.  Remmina und die notwendigen Plugins installieren:
    ```bash
    sudo apt update
    sudo apt install remmina remmina-plugin-vnc remmina-plugin-rdp
    [cite_start]``` [cite: 88, 89]
3.  [cite_start]**Vorbereitung Homeserver:** Sicherstellen, dass der Homeserver (Supermicro) einen Remote-Zugriffsservice (z.B. SSH, VNC-Server wie `xrdp` oder `vino-server`) installiert und konfiguriert hat. [cite: 90]

#### II.2. Erstellung eines Remote-Profils zum Homeserver

1.  [cite_start]Remmina starten und auf das `+`-Symbol klicken, um eine neue Remote-Sitzung zu erstellen. [cite: 92]
2.  **Basiseinstellungen:**
    * [cite_start]**Name:** Homeserver-Gaming / Homeserver-Verwaltung [cite: 94]
    * [cite_start]**Protokoll:** Je nach Konfiguration des Servers (z.B. **RDP** für Windows-VMs, **VNC** für Linux-Desktops oder **SSH** für die Shell-Verwaltung). [cite: 95]
    * [cite_start]**Server:** IP-Adresse des Homeservers eingeben (z.B. `192.168.x.x`). [cite: 96]
3.  **SSH-Tunneling (Sicherheitsaspekt):**
    * [cite_start]Optional: Auf den Reiter **SSH** wechseln und **"Enable SSH Tunnel"** aktivieren. [cite: 98]
    * [cite_start]Dies verschlüsselt die Verbindung zwischen Thin Client und Homeserver. [cite: 99]
    * [cite_start]SSH-Anmeldedaten (Benutzername/Passwort oder Schlüssel) des Homeservers eingeben. [cite: 100]
4.  [cite_start]**Verbindungstest:** Profil speichern und die Verbindung herstellen. [cite: 101]

---

### Phase III: Retro-Gaming-Umgebung

[cite_start]**Ziel:** Installation des RetroArch-Emulators und Einrichtung der Spielinhalte. [cite: 103]

#### III.1. Installation von RetroArch

[cite_start]RetroArch bietet die beste All-in-One-Lösung für Emulation auf Linux. [cite: 105]

1.  **Installation über Snap (Empfohlen für Aktualität):**
    * Terminal öffnen und RetroArch installieren:
        ```bash
        sudo snap install retroarch
        [cite_start]``` [cite: 109]
    * [cite_start]*Alternative:* Installation über die offiziellen Paketquellen. [cite: 110]
2.  **Erster Start und Grundeinrichtung:**
    * RetroArch starten. [cite_start]Standardmäßig wird eine Gamepad-freundliche Oberfläche angezeigt. [cite: 112]
    * [cite_start]Im Menü zu **"Online Updater"** navigieren. [cite: 113]
    * [cite_start]**"Core Downloader"** auswählen und die gewünschten Emulatorkerne (z.B. NES, SNES, PS1) herunterladen und installieren. [cite: 114]

#### III.2. Gamepad- und Hotkey-Konfiguration (A4)

1.  **Controller-Setup:**
    * [cite_start]Gamepad (Controller) an den Thin Client anschließen. [cite: 117]
    * [cite_start]Zu **"Settings → Input → Port 1 Controls"** navigieren und die Buttons neu zuordnen. [cite: 118]
2.  **Hotkeys (Komfort):**
    * [cite_start]Zu **"Settings → Input → Hotkeys"** gehen. [cite: 120]
    * [cite_start]Einen **Hotkey-Aktivator** (z.B. die Select-Taste) festlegen. [cite: 121]
    * [cite_start]Wichtige Funktionen wie **"Menü öffnen"** oder **"Save State"** mit Tastenkombinationen belegen, um die Steuerung ohne Tastatur zu ermöglichen. [cite: 122]

#### III.3. Einbindung der ROMs (Spieldaten)

[cite_start]Die ROMs werden zentral auf dem Homeserver gespeichert und über das Netzwerk in RetroArch eingebunden. [cite: 124]

1.  [cite_start]**Dateifreigabe vom Homeserver:** Sicherstellen, dass die ROMs auf dem Homeserver über **Samba (SMB)** oder **NFS** freigegeben sind (siehe Phase IV). [cite: 125]
2.  **In RetroArch:**
    * [cite_start]Zu **"Load Content"** navigieren. [cite: 127]
    * [cite_start]Die Netzwerkfreigabe (z.B. `/media/roms`) des Homeservers auswählen (der Thin Client muss diese Freigabe gemountet haben). [cite: 128]
    * [cite_start]Das gewünschte Spiel auswählen und mit **"Load Archive"** starten. [cite: 129]

---

### Phase IV: Datenintegration (Samba/NFS)

[cite_start]**Ziel:** Permanenter und sicherer Zugriff auf die Media- und ROM-Dateien auf dem Homeserver. [cite: 131]

#### IV.1. Homeserver-Konfiguration (Samba)

* [cite_start]**Voraussetzung:** Samba muss auf dem Homeserver (Xeon/256GB) installiert sein. [cite: 133]
* **Befehl (Homeserver):**
    ```bash
    sudo apt install samba
    [cite_start]``` [cite: 134]
* [cite_start]**Benutzer:** Separate Samba-Benutzer anlegen, die nicht direkt am System angemeldet werden können, aber Zugriff auf die Freigabe erhalten. [cite: 135]
    ```bash
    sudo useradd -s /bin/false -g users -m smbuser
    sudo smbpasswd -a smbuser
    [cite_start]``` [cite: 137, 138]
* [cite_start]**Freigabe definieren:** Die Konfigurationsdatei `/etc/samba/smb.conf` bearbeiten und einen Freigabebereich (z.B. `[RetroRoms]`) definieren. [cite: 139]

#### IV.2. Thin Client-Mount der Freigabe

[cite_start]Der Thin Client soll die Freigabe des Homeservers beim Systemstart automatisch einbinden (mounten). [cite: 141]

1.  **Installation des Clients:** Sicherstellen, dass das Samba-Client-Paket installiert ist:
    ```bash
    sudo apt install smbclient cifs-utils
    [cite_start]``` [cite: 142]
2.  **Mount-Punkt erstellen:** Ein lokales Verzeichnis als Mount-Punkt erstellen:
    ```bash
    sudo mkdir /mnt/homeserver_roms
    [cite_start]``` [cite: 143]
3.  [cite_start]**Permanentes Mounten (fstab):** Die `/etc/fstab` Datei bearbeiten, um die Freigabe automatisch beim Booten zu mounten. [cite: 144]
    ```bash
    //[SERVER_IP]/[FREIGABENAME] /mnt/homeserver_roms cifs credentials=/home/[USER]/.smbcredentials,uid=1000,gid=1000 0 0
    [cite_start]``` [cite: 146]
    * [cite_start]*Hinweis:* Die Datei `.smbcredentials` enthält den Benutzernamen und das Passwort für den Samba-Zugriff und muss sicher abgelegt werden. [cite: 147]

---

### Phase V: Medienwiedergabe und Feinjustierung

[cite_start]**Ziel:** Optimierung der YouTube-Wiedergabe und Beamer-Ausgabe. [cite: 149]

#### V.1. Medienwiedergabe (A3)

* [cite_start]YouTube wird über den bereits installierten Webbrowser (z.B. Firefox) abgespielt. [cite: 151]
* [cite_start]**Optimierung:** Bei Leistungsproblemen kann der **Homeserver** die Wiedergabe übernehmen: [cite: 152]
    * [cite_start]**Browser-Streaming:** Starten Sie den Browser auf einer Home-Server-VM und streamen Sie den gesamten Desktop via **Remmina** (VNC) oder **Parsec** zum Thin Client. [cite: 153]
    * [cite_start]**Vorteil:** Nutzt die dedizierte Rechenleistung des **Xeon** und der **AMD RX480** für das Rendering. [cite: 154]

#### V.2. Beamer-Ausgabe (A2)

1.  [cite_start]**Monitor-Einstellungen:** Nach dem Anschließen des Beamers die **"Monitor Settings"** in Lubuntu öffnen. [cite: 156]
2.  [cite_start]Die korrekte Auflösung des Beamers (für 720p/1080p/4K) auswählen. [cite: 157]
3.  [cite_start]**Anzeigemodus:** Den Modus auf **"Nur Beamer"** (Single Display) oder **"Erweitert"** (Extended Desktop) einstellen, je nachdem, ob der AIO-Bildschirm abgeschaltet werden soll. [cite: 158]
