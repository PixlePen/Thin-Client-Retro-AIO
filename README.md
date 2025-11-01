# Thin-Client-Retro-AIO
Thin Client "Retro-AIO": Wiederbelebung eines alten Lenovo F0B3 All-in-One PCs als Media- und Retro-Gaming-Client (PS1/Game Boy) über Lubuntu. Backend-Streaming-Fähigkeit via Homeserver (Xeon E5-2697v2, 256GB RAM, AMD RX480) zur Latenzkompensation und zentralen Datenhaltung.

# Thin-Client Projekt

**Von Dennis Nolden**

---

## 📝 Projektdokumentation: Thin Client für Retro-Gaming und Media-Wiedergabe

### 1. 🎯 Projektziele und Anforderungen

#### Executive Summary (Einleitung)

In diesem Projekt ist es mein Ziel, einen **Thin Client** zu erstellen aus bestehender alter Hardware (Lenovo F0B3 AIO PC), um in meinem Wohnzimmer **Retrogaming** und **Medienwiedergabe** (wie über YouTube) über einen Beamer zu ermöglichen. Die Anbindung erfolgt drahtlos an den zentralen Homeserver. 

| # | Ziel/Anforderung | Beschreibung |
| :--- | :--- | :--- |
| **P1** | Thin Client Funktion | Aufbau eines Thin Clients |
| **A1** | Hardware-Basis | Verwendung eines alten All-in-One (AIO) PCs (Lenovo F0B3) |
| **A2** | Bildausgabe | Bilddarstellung via Beamer |
| **A3** | Media-Wiedergabe | Wiedergabe von YouTube-Inhalten |
| **A4** | Retro-Gaming | Möglichkeit zum Spielen von Retro-Games |
| **A5** | Konnektivität | Verbindung zum Homeserver über WLAN |
| **A6** | Internetzugang | Vorhanden | 

---

### 2. 🖥️ Hardware-Basis und Infrastruktur

#### 2.1. Thin Client (AIO PC) – Frontend

| Komponente | Spezifikation | Rolle im Projekt |
| :--- | :--- | :--- |
| **Modell** | Lenovo F0B3 (AIO PC) | Frontend, lokaler Emulator-Host, Display-Ausgabe |
| **RAM** | 4 GB | Limitierende Ressource für anspruchsvolle Anwendungen |
| **Speicher** | 500 GB HDD-Festplatte | Lokaler Speicher für OS und Retro-Emulatoren/ROMs | 

#### 2.2. Homeserver (Backend)

| Komponente | Spezifikation | Rolle im Projekt |
| :--- | :--- | :--- |
| **CPU** | Intel(R) Xeon(R) CPU E5-2697 v2 @ 2.70GHz (12 Kerne) | Host für Virtualisierung, Game-Streaming-Server, Datenserver |
| **RAM** | 256 GB | Stellt ausreichend RAM für VMs, Container und Caching bereit |
| **GPU** | AMD RX480 | Dedizierte Grafikleistung für Transkodierung und/oder Gaming-Backend | 

---

### 3. 💻 Betriebssystem (OS) und Architekturentscheidung

#### 3.1. OS-Auswahl und Begründung (Thin Client)

| Option | Fokus | OS-Empfehlung | Begründung |
| :--- | :--- | :--- | :--- |
| **Fokus Allround** (Empfohlen) | YouTube & Thin Client | Lubuntu (LXQt) oder Xubuntu (XFCE) | Bieten eine optimale Balance aus Ressourcenverbrauch und Funktionalität (Webbrowser für YouTube, vollwertige Linux-Umgebung). 

#### 3.2. Implementierung der Kernfunktionen

| Funktion | Software/Implementierung | Details |
| :--- | :--- | :--- |
| **YouTube (A3)** | Aktueller Webbrowser | Wiedergabe hängt von der CPU/GPU des Lenovo AIO ab. |
| **Retro-Gaming (A4)** | RetroArch Emulator | All-in-One-Lösung für Konsolen (NES, SNES, PS1, etc.) auf dem AIO. |
| **Homeserver-Zugriff (A5)** | Remmina (Remote Desktop) | Tools für RDP, VNC, SSH (Administration), etc. auf Linux verfügbar. |
| **Dateizugriff** | Samba/NFS | Integration von Samba (Windows) oder NFS (Linux) Freigaben. |
| **Konnektivität** | WLAN (Wi-Fi) | Standardmäßig unterstützt von den genannten Linux-Systemen. 

---

### 4. 🚀 Rolle des Homeservers und Backend-Leistung

Der Homeserver dient als leistungsstarkes Backend, das die Schwächen des ressourcenlimitierten Thin Clients (4 GB RAM, schwächere lokale GPU) ausgleichen kann. 

| Einsatzszenario | Server-Komponente | Details zur Nutzung |
| :--- | :--- | :--- |
| **Erweiterte Emulation/Gaming** | Xeon CPU, 256 GB RAM | Hostet eine **Virtual Machine (VM)** oder Container, die per **Remote Desktop** (z.B. VNC oder Parsec) an den Thin Client gestreamt wird. |
| **Hardware-beschleunigtes Streaming** | AMD RX480 GPU | Ermöglicht GPU-Passthrough in eine Gaming-VM oder wird für die **Medien-Transkodierung** (z.B. Plex Media Server) verwendet. |
| **Zentrale Datenhaltung** | 256 GB RAM, HDD | Zentrale Speicherung aller Retro-ROMs und Media-Dateien. 

---

### 5. ⚠️ Risikobewertung (Hardware)

* **Leistungsgrenze (A3):** Die lokale Wiedergabe von HD- oder 4K-YouTube-Videos auf dem Thin Client (**Lenovo F0B3**) könnte aufgrund der älteren AIO-Hardware (CPU/GPU) an ihre Grenzen stoßen. 
    * **Lösung:** Nutzung des Homeservers für das Rendering und Streaming zum Client (z.B. via Parsec), um die Last auf die **AMD RX480** zu verlagern. 
* **WLAN-Latenz (A5, A4):** Die WLAN-Verbindung ist der kritische Pfad für Gaming-Streaming oder schnelle Remote-Desktop-Sitzungen. 
    * **Lösung:** Empfehlung, ein 5-GHz-Netzwerk (falls möglich) zu nutzen oder, für kritische Anwendungen, eine temporäre LAN-Verbindung in Betracht zu ziehen. 

---
---

## 📝 Umsetzungsanleitung: Thin Client für Retro-Gaming & Media-Wiedergabe

### Phase I: Vorbereitung und Installation des Thin Client OS

**Ziel:** Installation des schlanken Betriebssystems Lubuntu auf dem Lenovo F0B3 AIO PC. 

#### I.1. Systemanforderungen und Medienvorbereitung

* **Thin Client Hardware:** Lenovo F0B3 AIO PC (4 GB RAM, 500 GB HDD). 
* **OS-Wahl:** Lubuntu (aktuellste LTS-Version wird empfohlen). 
* **Installationsmedium:** USB-Stick (min. 8 GB) zur Erstellung eines bootfähigen Live-Systems. 
* **Vorgehen:**
    1.  Lubuntu ISO-Datei von der offiziellen Website herunterladen. 
    2.  Bootfähigen USB-Stick mit einem Tool wie Rufus oder Balena Etcher erstellen. 

#### I.2. Installation von Lubuntu

1.  **Booten:** AIO PC mit dem vorbereiteten USB-Stick starten. Ggf. im BIOS/UEFI die Bootreihenfolge anpassen. 
2.  **Live-System:** Im GRUB-Menü die Option "Try or Install Lubuntu" wählen. 
3.  **Installationsstart:** Auf dem Desktop auf das Icon "Install Lubuntu" klicken. 
4.  **Basiskonfiguration:** Sprache, Zeitzone und Tastaturlayout auf Deutsch festlegen. 
5.  **Partitionierung (Wichtig):**
    * Die Option **"Festplatte löschen und Lubuntu installieren"** wählen, da die alte Hardware als reiner Thin Client genutzt werden soll. 
    * *Alternativ (für Experten):* Manuelle Partitionierung, falls eine separate `/home` Partition gewünscht wird. Lubuntu benötigt ca. 8,5 GB freien Speicher. 
6.  **Benutzer anlegen:** Ersten Benutzer (mit Root-Rechten) und Passwort festlegen. 
7.  **Installation abschließen:** Nach Abschluss der Installation den PC neu starten und den USB-Stick entfernen. 

#### I.3. WLAN-Einrichtung (A5)

1.  Nach dem ersten Start auf dem Lubuntu-Desktop das **Netzwerk-Icon** in der Taskleiste (Panel) suchen. 
2.  Das gewünschte WLAN-Netzwerk (SSID) auswählen und das Passwort eingeben. 
3.  **Troubleshooting:** Sollte der WLAN-Adapter nicht erkannt werden:
    * Den AIO PC temporär per LAN-Kabel verbinden. 
    * Über das Terminal oder die **"Zusätzliche Treiber"**-Anwendung nach proprietären WLAN-Treibern suchen und diese installieren. 

---

### Phase II: Thin Client Funktionalität und Remoteverbindung

**Ziel:** Sicherstellung der Remote-Konnektivität zum Homeserver (Backend) zur Nutzung der Xeon/256GB/RX480-Ressourcen. 

#### II.1. Installation des Remote Desktop Clients (Remmina)

Der Remmina Remote Desktop Client wird für RDP/VNC/SSH-Verbindungen empfohlen. 

1.  Terminal öffnen (`Strg + Alt + T`). 
2.  Remmina und die notwendigen Plugins installieren:
    ```bash
    sudo apt update
    sudo apt install remmina remmina-plugin-vnc remmina-plugin-rdp
3.  **Vorbereitung Homeserver:** Sicherstellen, dass der Homeserver (Supermicro) einen Remote-Zugriffsservice (z.B. SSH, VNC-Server wie `xrdp` oder `vino-server`) installiert und konfiguriert hat. 

#### II.2. Erstellung eines Remote-Profils zum Homeserver

1.  Remmina starten und auf das `+`-Symbol klicken, um eine neue Remote-Sitzung zu erstellen. 
2.  **Basiseinstellungen:**
    * **Name:** Homeserver-Gaming / Homeserver-Verwaltung 
    * **Protokoll:** Je nach Konfiguration des Servers (z.B. **RDP** für Windows-VMs, **VNC** für Linux-Desktops oder **SSH** für die Shell-Verwaltung). 
    * **Server:** IP-Adresse des Homeservers eingeben (z.B. `192.168.x.x`). 
3.  **SSH-Tunneling (Sicherheitsaspekt):**
    * Optional: Auf den Reiter **SSH** wechseln und **"Enable SSH Tunnel"** aktivieren. 
    * Dies verschlüsselt die Verbindung zwischen Thin Client und Homeserver. 
    * SSH-Anmeldedaten (Benutzername/Passwort oder Schlüssel) des Homeservers eingeben. 
4.  **Verbindungstest:** Profil speichern und die Verbindung herstellen. 

---

### Phase III: Retro-Gaming-Umgebung

**Ziel:** Installation des RetroArch-Emulators und Einrichtung der Spielinhalte. 

#### III.1. Installation von RetroArch

RetroArch bietet die beste All-in-One-Lösung für Emulation auf Linux. 

1.  **Installation über Snap (Empfohlen für Aktualität):**
    * Terminal öffnen und RetroArch installieren:
        ```bash
        sudo snap install retroarch
    * *Alternative:* Installation über die offiziellen Paketquellen. 
2.  **Erster Start und Grundeinrichtung:**
    * RetroArch starten. Standardmäßig wird eine Gamepad-freundliche Oberfläche angezeigt. 
    * Im Menü zu **"Online Updater"** navigieren. 
    * **"Core Downloader"** auswählen und die gewünschten Emulatorkerne (z.B. NES, SNES, PS1) herunterladen und installieren. 

#### III.2. Gamepad- und Hotkey-Konfiguration (A4)

1.  **Controller-Setup:**
    * Gamepad (Controller) an den Thin Client anschließen. 
    * Zu **"Settings → Input → Port 1 Controls"** navigieren und die Buttons neu zuordnen. 
2.  **Hotkeys (Komfort):**
    * Zu **"Settings → Input → Hotkeys"** gehen. 
    * Einen **Hotkey-Aktivator** (z.B. die Select-Taste) festlegen. 
    * Wichtige Funktionen wie **"Menü öffnen"** oder **"Save State"** mit Tastenkombinationen belegen, um die Steuerung ohne Tastatur zu ermöglichen.

#### III.3. Einbindung der ROMs (Spieldaten)

Die ROMs werden zentral auf dem Homeserver gespeichert und über das Netzwerk in RetroArch eingebunden. 

1.  **Dateifreigabe vom Homeserver:** Sicherstellen, dass die ROMs auf dem Homeserver über **Samba (SMB)** oder **NFS** freigegeben sind (siehe Phase IV). 
2.  **In RetroArch:**
    * Zu **"Load Content"** navigieren. 
    * Die Netzwerkfreigabe (z.B. `/media/roms`) des Homeservers auswählen (der Thin Client muss diese Freigabe gemountet haben). 
    * Das gewünschte Spiel auswählen und mit **"Load Archive"** starten. 

---

### Phase IV: Datenintegration (Samba/NFS)

**Ziel:** Permanenter und sicherer Zugriff auf die Media- und ROM-Dateien auf dem Homeserver. 

#### IV.1. Homeserver-Konfiguration (Samba)

**Voraussetzung:** Samba muss auf dem Homeserver (Xeon/256GB) installiert sein. 
* **Befehl (Homeserver):**
    ```bash
    sudo apt install samba
* **Benutzer:** Separate Samba-Benutzer anlegen, die nicht direkt am System angemeldet werden können, aber Zugriff auf die Freigabe erhalten. 
    ```bash
    sudo useradd -s /bin/false -g users -m smbuser
    sudo smbpasswd -a smbuser
* **Freigabe definieren:** Die Konfigurationsdatei `/etc/samba/smb.conf` bearbeiten und einen Freigabebereich (z.B. `[RetroRoms]`) definieren. 

#### IV.2. Thin Client-Mount der Freigabe

Der Thin Client soll die Freigabe des Homeservers beim Systemstart automatisch einbinden (mounten). 

1.  **Installation des Clients:** Sicherstellen, dass das Samba-Client-Paket installiert ist:
    ```bash
    sudo apt install smbclient cifs-utils
2.  **Mount-Punkt erstellen:** Ein lokales Verzeichnis als Mount-Punkt erstellen:
    ```bash
    sudo mkdir /mnt/homeserver_roms
3.  **Permanentes Mounten (fstab):** Die `/etc/fstab` Datei bearbeiten, um die Freigabe automatisch beim Booten zu mounten. 
    ```bash
    //[SERVER_IP]/[FREIGABENAME] /mnt/homeserver_roms cifs credentials=/home/[USER]/.smbcredentials,uid=1000,gid=1000 0 0
    *Hinweis:* Die Datei `.smbcredentials` enthält den Benutzernamen und das Passwort für den Samba-Zugriff und muss sicher abgelegt werden.

---

### Phase V: Medienwiedergabe und Feinjustierung

**Ziel:** Optimierung der YouTube-Wiedergabe und Beamer-Ausgabe. 

#### V.1. Medienwiedergabe (A3)

YouTube wird über den bereits installierten Webbrowser (z.B. Firefox) abgespielt. 
**Optimierung:** Bei Leistungsproblemen kann der **Homeserver** die Wiedergabe übernehmen: 
*Browser-Streaming:** Starten Sie den Browser auf einer Home-Server-VM und streamen Sie den gesamten Desktop via **Remmina** (VNC) oder **Parsec** zum Thin Client. 
    * **Vorteil:** Nutzt die dedizierte Rechenleistung des **Xeon** und der **AMD RX480** für das Rendering. 

#### V.2. Beamer-Ausgabe (A2)

1.  **Monitor-Einstellungen:** Nach dem Anschließen des Beamers die **"Monitor Settings"** in Lubuntu öffnen. 
2.  Die korrekte Auflösung des Beamers (für 720p/1080p/4K) auswählen. 
3.  **Anzeigemodus:** Den Modus auf **"Nur Beamer"** (Single Display) oder **"Erweitert"** (Extended Desktop) einstellen, je nachdem, ob der AIO-Bildschirm abgeschaltet werden soll. 
