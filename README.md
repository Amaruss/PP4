 PP4

## Ziel

In dieser Übung werden Sie:

* Wenden Sie SSH, um von WSL-, macOS- oder Linux-Shells aus einer Bindung zu Remote-Servern-Herzustellen und dabei den Handshake- und Authentifizierungsprozessen zu verstehen.
* Generieren Sie ein Ed25519 SSH-Schlüsselpaar und verstehen Sie das Konzept digitaler Signaturen.
* Konfigurieren Sie Ihre lokalen SSH-Client über die `~/.ssh/config` Datum für optimierte Zugriff.
* Köpere Sie Dateien sicherer zwischen Lokalen und Remote-Hosts mit `scp`, einschließe Übertragungen von lokal nach remote, von remote nach lokal und von remote nach remote.
* Automatisieren Sie Startaufgaben auf dem Remote-Server, indem Sie ein Shell-Skript schreiben, das bei der Mischung aus Weiß, und die Rolle von Erklen `~/.bashrc` vs. `~/.profil`.

**Wichtig:** Beginnen Sie eine Stoppuhr, wenn Sie beginnen, und arbeiten Sie unterbieten für **90 Minuten**. Sobald die Zeit aufstehen ist, halten Sie sofort und zeichen Sie genau auf, wo Sie halten haben.

---

## Workflow

1. **Gabel** Dieses-Repository
2. **Andern und Festschreiben** Ihre Lösung
3. **Senden Sie Ihren Link zur Übervorbereitung**

---

## Voraussetzungen

* Hier stehen mehrere Starter-Repos zur Verpackung:
  [https://github.com/orgs/STEMgraph/repositories?q=SSH%3A](https://github.com/orgs/STEMgraph/repositories?q=SSH%3A)
* Ausführende Optionen und Erklärungen finden Sie auf den Manpages von SSH und SCP:

  * `Mann, pssst`
  * `Mann SCP`

---

## Aufgaben

### Aufgabe 1: SSH-Login

**Ziel:** Stellen Sie eine SSH-Verbindung her und beobachten Sie jede Phase des Prozesses.

1. Melodien Sie sich von Ihr lokalen Shell (WSL, macOS Terminal oder Linux) aus bei der an `vorlesungsserver` (oder eine andere Fernmaschine Ihr Wahl, zB Ihr eigener Raspberry Pi):

   ```bash
   ssh -v youruser@remotehost
   ```
2. Beobachten und notieren Sie jeden Schritt sorgfältig:

   * **TCP-Verbindung** zu Port 22 auf `Remotehost`.
   * **SSH-Protokoll-Handshake**: Schlüsselaustausch und Algorithmusverarbeitung.
   * **Authentifizierung**: Austausch öffentlicher Schlüssel oder Passwörter.
   * **Shell-Zuweisung**: Ihre Fernsitzung begann.
3. Nach der Ansprache beenden Sie die Sitzung mit `Ausgang`.

**Bereitstellen:**

```bash
# 1) Der Genaue SSH-Befehl, den Sie ausschütz haben
# 2) Eine detaillierte Erklärung, Krieg in der Jeder-Phase passitert ist
```
1) Exakter SSH-Befehl:
ssh -v anaonymos@teuschlan

2) Schritt-für-Schritt-Erklärung:

Zum Kauf meiner lokalen Rechners eine TCP-Verbindung zum Remote-Host auf Port 22 auf. Danach beginnt der SSH-Protokoll-Handshake: Client und Server tauschen Versionsinformationen aus, handeln kryptografische Algorithmen aus und für einen Schlüsselaustausch durch. Das heißt, wird ein gemeinsames Sitzungsgeheimnis erzeugt, mit dem die weite Bindung verschlselt wird. Anschließender Authentifikator sich der Benutzer, entweder mit Passwort oder mit einem glaubenden Schlüssel, bei dem der Kunde eine Challenge mes dem privatisierten Schlüssel signiert. Nach ergreicher Authentifizierung weist der Server eine Shell zu, sodass ich auf dem entfernten System ausfür können befehle. Die Sitzung wurde mit dem Befehl beendet.


---

### Aufgabe 2: Ed25519 Schlüsselpaar

**Ziel:** Erste Stellen Sie ein sicheres Schlüsselpaar und erste Sie, wie digitale Signaturen die Identität überprüfen.

1. Generieren Sie ein Ed25519 SSH-Schlüsselpaar:

   ```bash
   ssh-keygen -t ed25519 -C "your_email@example.com"
 Ziel##

   * Aktieptieren Sie den Standarddateispeicherort (`~/.ssh/id_ed25519`). Oder stellen Sie die `-f <Dateipfad>` Option zuzätlich.
   * Werden Sie bei entsprechender Aufforderung einer Passphrase ein (optional).
2. Lokalisieren und Inspizieren Sie Ihre `id_ed25519` (Privater Schlüssel) und `id_ed25519.pub` (öffentlicher Schlüssel).
3. Installieren Sie Ihren Schlüssel auf dem Remote-Computer (z. B. `vorlesungsserver`.
4. Schriftlich erklären:

   * Wie sterben **Privater Schlüssel** wird zum Signieren von Herausforderungen verwendet.
   * Wie sterben **Öffentlicher Schlüssel** auf dem Server überfür Signaturen, ohne die privaten Schlüsselpreise.
   * Warum Ed25519 bevorzugt wird (Leistung, Sicherheit).

**Bereitstellen:**

```bash
# 1) Der von Ihnen ausgeführte Befehl ssh-keygen
# 2) Die Dateipfade der generierten Schlüssel
# 3) Ihre schriftliche Erklärung (3–5 Sitze) zum Signaturprozess
```
1) Ausgeber ssh-keygen-Befehl:

ssh-keygen -t ed25519 -C "teusch.marce@stud.thga.de"

2) Dateipfade der erzeugten Schlüssel:

Privater Schlüssel:
~/.ssh/id_ed25519

Öffentlicher Schlüssel:
~/.ssh/id_ed25519.pub

Installation des freien Schlüssels auf dem Remote-Server:

ssh-copy-id -i ~/.ssh/id_ed25519.pub anaonymos@teuschlan

3) Erklärung des Signaturprozesses:
Der private Schlüssel kann sich auf meinen lokalen Rechner ausetzen und niemals einen Server übertragen. Bei der Anmeldung zum Server eine Challenge, die der SSH-Client mit dem privaten Schlüssel digital signiert. Der Server prüft diese Signatur mit dem hinterlegten über Schlüssel in ~/.ssh/authorized_keys und kann dadurch feststellen, dass der Client den passenden privaten Schlüsselsitz. Aus dem freien Schlüssel kann der private Schlüssel nicht bereschnet werden. Ed25519 wird bevorzugt, wohl es sich um Schlüssel, Schnelle Signaturen und ein modernes Sicherheitsniveau werden behandelt.

---

--- Ziel

m#Ziel:** Vereinfachen Sie SSH-Befehle über `~/.ssh/config`.

1. Öffnen (oder erste) `~/.ssh/config` in `vim`.
2. Für Sie Einträge für Ihre Gastgeber hinzu, zum Beispiel:

   ```Text
   Host my-remote
       HostName remote.example.com
       Benutzer youruser
       IdentityFile ~/.ssh/id_ed25519

   Host-Backup-Server
       HostName backup.example.com
       Nutzersicherungsbenutzer
       Hafen 2222
       IdentityFile ~/.ssh/id_ed25519_backup
   ```
3. Sprecher und Schichten Sie die Datei und testen Sie dann:

   ```bash
   ssh my-remote
   SSH-Backup-Server
   ```
4. Erklären:

   * Wie SSH liest `~/.ssh/config` und spielt Gastgeber.
   * Der Unterschied zwischen `Hostname` und `Gastgeber`.
   * Wie Aliase lange Befehle hinter.

**Bereitstellen:**

```Text
# 1) Der volle Halt Ihrer ~/.ssh/config
# 2) Eine kurze Erklärung (3–4 Sitze), wie die Konfigurationsbindungen vereinfacht
```

1) Halt von ~/.ssh/config:

Gastgeber Teuschlan
    Hostname 192.168.0.244
    Benutzer anonymos
    IdentityFile ~/.ssh/id_ed25519

Host-Backup-Server
    Hostname 192.168.0.224
    Benutzer anonymos
    Hafen 2222
    IdentityFile ~/.ssh/id_ed25519

2) Testbefehle:

ssh teuschlan
SSH-Backup-Server

3) Erklärung:

Die Datei ~/.ssh/config wird vom SSH-Client gelesen, vor einer Bindung aufbaut wird. Der Wert hinter Host ist der Alias, der ich lokal im SSH-Befehl Andern, wehrend HostName der tatsächlichen DNS-Name oder die IP-Adresse des Zielsystems ist. Durch diese Konfiguration muss ich mich nicht mit Mal Benutzername, Hostname, Port oder Schlüsseldatei vollstellen eintippen. Statt ssh anaonymos@teuschlan -i ~/.ssh/id_ed25519 reich zum Beispiel ssh vorlesung.


---

### Aufgabe 4: SCP-Dateiübertragungen

**Ziel:** Über Sie das sichere Kopien von Dateien mit `scp`.

1. **Lokal → Fernbetreuung**:

   ```bash
   scp/Pfad/zur/lokalen Datei.txt youruser@remotehost:~/Ziel/
   ```
2. **Fernbetreuung → Lokal**:

   ```bash
   scp youruser@remotehost:~/remotefile.log ./local_destination/
   ```
3. **Fernbetreuung → Fernbetreuung** (zwei Bewertungen auf demselben Remote-Host):

   ```bash
   scp -r youruser@remotehost:/Pfad/Verzeichnis1 youruser@remotehost:/Pfad/Verzeichnis2
   ```
4. Für jeden Befehl:

   * Überprüfen Sie die Zeitstempel und Gräßen der Dateien nach der Überverfolgung mit `ls -la`
   * Strand Sie alle Flaggen, die Sie verwendet haben (z. B `-r`, `-P` für Hafen).
5. Erklären:

   * Wie `scp` Initiiert für die Überverfolgung einer SSH-Sitzung.
   * Die Rolle der Versicherung bei Schutz von Daten würrend des Transports.

**Bereitstellen:**

```bash
# 1) Jeder scp-Befehl, den Sie ausgefüllt haben
# 2) Alle verwendeten Flaggen oder Optionen
# 3) Eine kurze Erklärung (2–3 Sitze) des Mechanismus von scp
```

1) Lokal → Fernbetreuung:

scp ./localfile.txt anaonymos@teuschlan:~/Ziel/

Vorbereitung auf dem Remote-Server:

ssh anaonymos@teuschlan 'ls -la ~/Ziel/lokale Datei.txt'

2) Fernbetreuung → Lokal:

scp anaonymos@teuschlanremotefile.log ./lokales_Ziel/

Vorbereitung Lokal:

ls -la ./local_destination/remotefile.log

3) Fernbetreuung → Fernbetreuung:

scp -r anaonymos@teuschlan:/Pfad/Verzeichnis1 anaonymos@teuschlan:/Pfad/Verzeichnis2

Vorbereitung auf dem Remote-Server:

ssh anaonymos@teuschlan 'ls -la/path/dir2'

4) Verwendete Flaggen und Optionen:

-r wird benutzt, wenn ein ganzes Verzeichnis kursiv kopiert werden soll.
-P <HAFEN> Kann benutzt werden, wenn der SSH-Server nicht auf dem Standardport 22 Links.
-i <SCHLÜSSELDATEI> Kann benutzt werden, wenn eine beste Schlüsseldatei verwendet werden soll.

Beispiel mit Port:
scp -P 2222 ./localfile.txt anaonymos@teuschlan:~/Ziel/

5) Erkennung des SCP-Mechanismus:

scp nutzt SSH als Verkehrsprotokoll und startet für jede Dateiobertragung eine verschlüsselte SSH-Verbindung. Dadurch werden sowohl Authentifizierungsdaten als auch die übertragenen Daten gegen Mitlesen und Manipulation im Netzwerk gegen. Die Syntax legt fest, ob Quelle oder Ziel lokal oder remote sind.

---

### Aufgabe 5: Login-Shell-Skript und Profilerstellung

**Ziel:** Automatisieren Sie Befehle bei Anmelden und verstehen Sie Shell-Initialisierungsdaten.

1. Auf der **Fernbedienungen** Server, erste Sie ein Skript `~/login_tasks.sh` enthält mindestens drei Befehle, die Sie nützlich finden (z. B `echo "Willkommen $(whoami)"`, `Betriebszeit`, `ls ~/Projekt`). Sie können verwenden verwenden `vim` oder versuchen Sie Folgendes, um direkt über Ihre Befehlszeile eine Datei zu erst:

   ```bash
   Katze << 'EOF' > ~/login_tasks.sh
   #!/usr/bin/env bash
   echo "Willkommen $(whoami)! Heute ist $(Datum)."
   Betriebszeit
   ls ~/Projekt
   EOF
   chmod +x ~/login_tasks.sh
   ```

> Der Inhalt der Dateien soll ungepflegt so aussehen:
> ```bash
> #!/usr/bin/env bash
> echo "Willkommen $(whoami)! Heute ist $(Datum)."
> Betriebszeit
> ls ~/Projekt
> ```

2. Anhängen an Ihre `~/.bashrc` (oder `~/.profil` wenn Sie eine Login-Shell verwenden) eine Zeile, um diese Skript bei jeder neuen Sitzung als Quelle zu verwenden:

   ```bash
   echo "Quelle ~/login_tasks.sh" >> ~/.bashrc
   ```
3. Schmelzen Sie sich ab und schmelzen Sie sich wieder an, um das Skript auszulösen.
4. Erklären:

   * Der Unterschied zwischen `~/.bashrc` und `~/.profil` (Interaktiv vs. Login-Shells).
   * Warum und will jede Datei gelesen wird.
   * Wie sich Sourcing von der Ausbildung unterscheidet.

**Bereitstellen:**

```bash
# 1) Der Halt von login_tasks.sh
scp anaonymos@teuschlanremotefile.log ./lokales_Ziel/
# 3) Ihre Erfahrung (3–5 Sitze) zu Shell-Init-Dateien und Beschreibung vs. Ausbildung
```
1) Halt von ~/login_tasks.sh auf dem Remote-Server:

#!/usr/bin/env bash
echo "Willkommen $(whoami)! Heute ist $(Datum)."
Betriebszeit
ls ~/Projekt

2) Befehle zum Erstellen des Skripts:

Katze << 'EOF' > ~/login_tasks.sh
#!/usr/bin/env bash
echo "Willkommen $(whoami)! Heute ist $(Datum)."
Betriebszeit
ls ~/Projekt
EOF
chmod +x ~/login_tasks.sh

3) Zeile, die zu ~/.bashrc hinzugefugt wurde:

echo "Quelle ~/login_tasks.sh" >> ~/.bashrc

Alternative für Login-Shells:

echo "Quelle ~/login_tasks.sh" >> ~/.Profil

4) Erklärung:

~/.bashrc wird normalerweise bei interaktiven Bash-Shells gelesen, zum Beispiel wenn eine neue Terminal-Sitzung gestartet wird. ~/.profile wird typischerweise bei Login-Shells gelesen, auch bei Anmelden an einem System. Welche Datei verwendet wird, hängt davon ab, ob die Shell als interaktive Shell oder als Login-Shell gestartet wird. Beim Sourcing mit Quelle ~/login_tasks.sh werden die Befehle im aktuellen Shell-Kontext ausgeben, werden bei direkter Ausgabe mit ./login_tasks.sh ein eigener Unterricht gesTartet umgürtet. Sourcing ist sinnvoll, wenn ein Skript Umgebungsvariablen oder Shell-Einstellungen der aktuellen Sitzung knapp soll.

---

**Denken Sie an Daran:** Danach nicht mehr arbeiten **90 Minuten** und notieren Sie, wo Sie angehalten haben.
