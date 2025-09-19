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
