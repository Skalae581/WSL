# WSL und Docker – Kurz & Klar

## Was ist WSL?

**WSL (Windows Subsystem for Linux)** ist eine integrierte Linux-Umgebung unter Windows.  
Du bekommst „echtes“ Linux (z. B. Ubuntu) ohne VM-Overhead. Dateien und Prozesse lassen sich zwischen Windows und Linux teilen.

---

## Wofür nutzt man es?

- Linux-Tools unter Windows (git, bash, apt, python, make …)  
- Dev-Stacks, die Linux erwarten (Node, Python, Java, Docker, Kubernetes)  
- Bessere I/O-Performance als klassische VMs/Hyper-V-VMs  

---

## Wie nutze ich WSL mit Docker?

### 1) Voraussetzungen prüfen

PowerShell (Admin):

```powershell
wsl --version          # sollte 2.x anzeigen
wsl --list --online    # verfügbare Distros
wsl --install -d Ubuntu
```

Nach der Installation einmal Windows neu starten, Ubuntu öffnen, Benutzer anlegen.

---

### 2) Docker Desktop mit WSL koppeln

* **Docker Desktop → Settings → Resources → WSL Integration**

  * „**Enable integration with my default WSL distro**“ aktivieren
  * Bei Bedarf Ubuntu anhaken
* **General**: „Use the WSL 2 based engine“ aktivieren

---

### 3) Test

In **PowerShell** oder **Ubuntu (WSL)**:

```bash
docker --version
docker run hello-world
```

Wenn „Hello from Docker!“ erscheint, läuft’s ✅.

---

### 4) Dein Projekt starten (TaskHub-Beispiel)

In PowerShell/WSL ins Projektverzeichnis:

```bash
cd taskhub
docker compose -f docker-compose.dev.yml up --build
# Prod:
# docker compose up --build -d
```

* Frontend: [http://localhost:5173](http://localhost:5173) (dev) / [http://localhost:8080](http://localhost:8080) (prod)
* Backend:  [http://localhost:4000/api/health](http://localhost:4000/api/health)

---

## Nützliche Hinweise

* **Dateipfade:** Arbeite fürs beste Tempo **innerhalb WSL** (z. B. `/home/<user>/projects`), nicht auf `C:\` gemounteten Ordnern.
  Zugriff von Windows auf WSL-Dateien: `\\wsl$\Ubuntu\home\<user>\projects`

* **Volumes:** Benutze Docker-Volumes statt Host-Bind-Mounts auf `C:\` für mehr Performance.

* **Port-Zugriff:** Dienste in WSL/Docker sind über `localhost:<port>` in Windows erreichbar.

* **WSL aktualisieren:**

  ```powershell
  wsl --update
  ```

  Kernel manuell: [https://aka.ms/wsl2kernel](https://aka.ms/wsl2kernel)

* **Neustarten:**

  ```powershell
  wsl --shutdown
  ```

  beendet alle Distros; dann Docker Desktop neu öffnen.

---
