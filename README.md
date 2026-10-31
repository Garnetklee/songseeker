# songseeker
A Music Guessing game called SongSeeker, available as Website.

Just provide the contents on some https page and you should be good to go (camera access via http is often not allowed).

Example is available at https://songseeker.grub3r.io/

Inspired from https://hitstergame.com/de-de/ and https://rockster.brettspiel.digital/

Youtube links from the original Hitster cards get be downloaded from https://github.com/andygruber/songseeker-hitster-playlists

qr-scanner from https://github.com/nimiq/qr-scanner

### Generating QR-Code Gamecards

https://github.com/andygruber/songseeker-card-generator

### Docker image build

```
docker build -t songseeker -f .\imagebuild\Dockerfile .
```
## Eigene Karten (Fork Garnetklee)

Dieser Fork kann eigene Karten abspielen, deren QR-Code nur eine Kartennummer enthält:

```
https://garnetklee.github.io/songseeker/?c=ktv01-042
```

- `ktv01` ist das Set, die App lädt dafür `playlists/ktv01.csv` (Kopf `Card#,URL`, eine Zeile je Karte, z. B. `042,https://youtu.be/<id>?t=12`).
- Gefunden wird die Nummer mit oder ohne führende Nullen (`042` = `42`), Groß- und Kleinschreibung beim Set egal.
- Mit SongSeeker gescannt: spielt wie ein YouTube-Link. Mit der normalen Kamera gescannt: die Seite öffnet sich, lädt die Karte und zeigt einen großen Play-Knopf.
- Titel, Video-ID und Dauer werden bei eigenen Karten nie angezeigt. Fehlt eine Nummer oder ist das Video nicht abspielbar, erscheint eine Meldung nur mit der Kartennummer.
- Neues Set: einfach `playlists/<set>.csv` hinzufügen, die QR-Codes lauten dann `?c=<set>-<nr>`.

### Liste aktualisieren

1. `playlists/ktv01.csv` ersetzen (z. B. totes Video gegen neuen Link tauschen), committen und pushen.
2. GitHub Pages veröffentlicht nach ca. 1 Minute (Reiter „Actions“ zeigt den Lauf).
3. Kein Service Worker; die App lädt die CSV mit `cache: "no-cache"`, Änderungen kommen also beim nächsten Seitenaufruf an.
   Nur bei Änderungen an `app.js` die Versionsnummer in `index.html` (`app.js?version=…`) hochzählen.

Die offiziellen Hitster-Playlists liegen nicht in diesem Repo (das Docker-Image lädt sie aus `andygruber/songseeker-hitster-playlists`), auf GitHub Pages funktionieren offizielle Hitster-Karten daher nicht. Direkte YouTube-Links funktionieren.
