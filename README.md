# Solar Interference

*Light is both particle and wave. Let a field of suns ripple like one.*

Generative Wellenfeld-Visualisierung: ein Interferenzfeld wird in ein Raster
quantisiert und dort als kreisförmige Pixel oder als Bilder gezeichnet — ein Bild
je Helligkeitsstufe.

Die Schriften liegen im Ordner `fonts/` und werden vom eigenen Server geladen —
keine Anfrage an Google, damit auch kein Datenschutzthema.

Die Oberfläche gibt es auf **Englisch und Deutsch**; Englisch ist die Vorgabe. Der
Knopf oben links neben dem Theme-Schalter wechselt, und die Wahl bleibt im Browser
gespeichert. Name und Untertitel stehen in beiden Sprachen gleich.

Alles steckt in `index.html`. Kein Build, kein Bundler, keine Abhängigkeit außer
p5.js vom CDN.

> **Vor dem ersten Teilen:** In `index.html` stehen ganz oben zwei Adressen mit
> `DEINNAME` darin (`og:url` und `og:image`, dazu einmal für Twitter). Die auf die
> eigene GitHub-Pages-Adresse ändern — sonst zeigen Social-Media-Dienste kein
> Vorschaubild.

```
solar-interference/
├── index.html      ← die App
├── images.json     ← welche Bilder es gibt und welche Stufe sie belegen
├── preview.jpg          ← Vorschaubild beim Teilen (1200 × 630)
├── apple-touch-icon.png ← Home-Bildschirm-Icon fürs iPhone (180 × 180)
├── icon-192.png         ← Home-Bildschirm-Icon für Android
├── icon-512.png         ← dasselbe in groß
├── site.webmanifest     ← Name und Icons für Android/PWA
├── fonts/               ← die vier Schriftschnitte
└── img/                 ← die Bilddateien
```

`images.json` und `img/` entstehen erst, wenn du das erste Mal veröffentlichst.
Ohne sie startet die App mit leerer Bibliothek — alles andere funktioniert.

---

## 1 · Auf GitHub Pages veröffentlichen

```bash
git init
git add index.html README.md
git commit -m "Solar Interference"
git branch -M main
git remote add origin git@github.com:DEINNAME/solar-interference.git
git push -u origin main
```

Im Repo: *Settings* → *Pages* → Source **Deploy from a branch**, Branch `main`,
Ordner `/ (root)` → *Save*. Nach etwa einer Minute liegt die Seite unter
`https://DEINNAME.github.io/solar-interference/`.

---

## 2 · Wer darf was

**Alle Besucher** sehen dieselben Bilder aus dem Repository, können alle Parameter
verstellen, exportieren und Einstellungen teilen. Bibliothek, Upload und Admin
bleiben bei ihnen unsichtbar.

**Du** siehst zusätzlich die Bibliothek und den Admin-Bereich. Die erscheinen,
sobald in diesem Browser ein Token liegt — oder wenn du die Seite mit `?admin=1`
aufrufst:

```
https://DEINNAME.github.io/solar-interference/?admin=1
```

Das ist keine Sicherheitsschranke, sondern nur Aufräumen der Oberfläche: Schreiben
kann ohnehin nur, wer ein gültiges Token besitzt. Zwei Wege dafür, beide erzeugen
dasselbe Ergebnis:

### Weg A — ohne alles: ZIP

In der Bibliothek auf **↓ ZIP** klicken. Die Datei enthält `images.json` und den
kompletten `img/`-Ordner. Entpacken, Inhalt bei GitHub in das Repository ziehen,
fertig. Funktioniert immer, auch wenn ein Token fehlt oder abgelaufen ist.

### Weg B — mit Token: direkt aus der Seite heraus

Ein Klick auf **↑ Ins Repository veröffentlichen** committet die neuen Bilder und
das Manifest selbst. Dafür brauchst du einmalig ein GitHub-Token.

**Token erstellen**

1. GitHub → Profilbild → *Settings* → ganz unten *Developer settings*
2. *Personal access tokens* → **Fine-grained tokens** → *Generate new token*
3. **Repository access**: *Only select repositories* → dein `solar-interference`
4. **Permissions** → *Repository permissions* → **Contents**: `Read and write`
   (mehr nicht — alles andere bleibt auf *No access*)
5. **Expiration**: 90 Tage oder *No expiration*. Läuft es ab, funktioniert nur
   noch Weg A, bis du ein neues erstellst.
6. *Generate token* → die Zeichenkette wird **nur einmal** angezeigt, direkt kopieren

**Token hinterlegen**

Auf der Seite im Bereich *Admin* einfügen und *Token merken* klicken. Benutzername
und Repository liest die Seite selbst aus der Adresse; überschreiben kannst du sie
in den Feldern darunter.

Das Token liegt danach ausschließlich in diesem einen Browser (`localStorage`).
Es steht nirgends im Quelltext und kommt nie ins Repository — andere Besucher
sehen bei sich einfach leere Felder und können nicht veröffentlichen. Auf einem
zweiten Gerät fügst du es erneut ein. Landet es je irgendwo, wo es nicht hingehört:
bei GitHub unter *Fine-grained tokens* mit einem Klick widerrufen. Weiter als in
dieses eine Repository kommt damit niemand.

Nach dem Veröffentlichen dauert es ~40 Sekunden, bis GitHub Pages die neue Fassung
ausliefert.

---

## 3 · Teilen auf Social Media

`index.html` bringt Open-Graph- und Twitter-Card-Angaben mit: Titel, Beschreibung
und das Vorschaubild `preview.jpg`. Damit erscheint beim Posten eine Karte statt
eines nackten Links. **Die absoluten Adressen im Kopf der Datei müssen angepasst
werden** — Facebook, LinkedIn und Co. lesen keine relativen Pfade.

Das mitgelieferte `preview.jpg` ist 1200 × 630 groß. Ersetzen kannst du es
jederzeit durch einen eigenen Export; behalte dann diese Maße bei, sonst stimmen
die beiden Angaben `og:image:width` und `og:image:height` nicht mehr.

Prüfen lässt sich das Ergebnis vor dem Posten mit den Debuggern der Plattformen
(bei Facebook „Sharing Debugger", bei LinkedIn „Post Inspector"); die zeigen auch,
ob ein alter Zwischenspeicher noch eine frühere Fassung ausliefert.

**Home-Bildschirm-Icon** — Legt jemand die Seite auf dem iPhone als Verknüpfung ab
(*Teilen → Zum Home-Bildschirm*), erscheint `apple-touch-icon.png` als App-Icon,
darunter der Name „Solar Interference"; die runden Ecken fügt iOS selbst hinzu.
Android nimmt die Icons aus `site.webmanifest`. Alle vier Dateien gehören ins
Repo-Wurzelverzeichnis neben `index.html`; ein eigenes Motiv einfach unter
denselben Namen ablegen (iPhone 180 × 180, Android 192 und 512).

**Belastbarkeit** — Es gibt keinen Server und keine Datenbank: Jeder Besucher
rechnet auf dem eigenen Gerät. Über dein Kontingent läuft nur die Auslieferung der
Dateien, rund 1,1 MB je Erstbesucher (p5.js kommt vom fremden CDN und zählt nicht
mit). Bei den 100 GB Monatsvolumen von GitHub Pages sind das etwa 95.000
Erstaufrufe; Wiederkehrer kosten dank Zwischenspeicher fast nichts. Und es ist ein
*soft limit* — GitHub meldet sich, statt abzuschalten.

---

## 4 · Bilder

Beim Hochladen verkleinert der Browser jedes Bild auf 640 px lange Kante und
komprimiert es — WebP, oder PNG wenn Transparenz im Spiel ist. Ein Bild landet
damit typischerweise bei 30–80 KB; 30 Bilder wiegen zusammen etwa 1,5 MB und
werden vom Browser einzeln zwischengespeichert.

In `images.json` steht neben der Dateiliste auch die Zuordnung Stufe → Bild,
getrennt nach Stufenanzahl: eine Belegung für 10 Stufen und eine für 16 Stufen
können nebeneinander bestehen. Änderst du die Stufenzahl, greift automatisch die
dort hinterlegte Belegung. Kennt das Manifest eine Stufenzahl nicht, verteilt die
Seite die Bibliothek selbst gleichmäßig über die Stufen und übernimmt dabei die
Richtung aus den vorhandenen Belegungen — jede Stufenzahl von 2 bis 30 ist also
nutzbar, auch ohne passenden Eintrag. Beim Veröffentlichen bleiben die Belegungen
der übrigen Stufenzahlen erhalten.

Bilder sind der Normalfall: Sind welche hinterlegt, werden sie benutzt. Stufen
ohne Bild fallen auf Kreise zurück, und ohne Bibliothek zeichnet die Seite
durchgehend Kreise — die Punkte sind also die Rückfalllösung, nicht umgekehrt.

Weil die Bilder aus demselben Repository kommen wie die Seite, funktionieren
PNG- und Video-Export ohne Einschränkung. Bilder von fremden Servern würden das
Canvas sperren und den Export unmöglich machen — deshalb liegen sie hier.

**Wenn Bilder nicht erscheinen**, sagt die Statuszeile unter der Bibliothek, woran
es liegt:

| Meldung | Bedeutung |
|---|---|
| `images.json nicht gefunden — erwartet unter …` | Die Datei liegt nicht neben `index.html`. Der genannte Pfad ist der, an dem gesucht wird. |
| `12 von 34 Bildern fehlen — img/solar-1.jpg nicht gefunden (404)` | Das Manifest wurde gelesen, die Datei liegt aber nicht unter diesem Pfad. Betroffene Bilder sind in der Bibliothek gestrichelt mit `!` markiert. |
| `… mit abweichender Dateiendung gefunden` | Alles geladen, aber die tatsächliche Endung war eine andere als im Manifest — etwa `.JPG` statt `.jpg`. |

Der letzte Fall wird automatisch aufgelöst: GitHub Pages unterscheidet Groß- und
Kleinschreibung, weshalb `solar-1.JPG` nicht auf `img/solar-1.jpg` antwortet. Die
Seite probiert deshalb die üblichen Schreibweisen durch und meldet, welche
funktioniert hat. Die vollständige Liste fehlender Dateien steht in der
Browser-Konsole.

---

## 5 · Bedienung

**Wellenfeld** — Vier Wellenfronten: *Radial* (Punktquellen, die sich
durchdringen), *Linear* (ebene Fronten mit Winkel und Fächerung), *Gemischt* und
*Zentrisch* (Ringe und Spiralarme). Das **Wellenprofil** bestimmt die Form der
Welle: Sinus weich, Rechteck mit harten Kanten, dazu Dreieck und Sägezahn.
**Spiegelachsen** faltet das Feld kaleidoskopisch in 2 bis 12 Sektoren.

**Bewegung** — Normalerweise wandert das Muster. Mit **Stehende Welle** bleibt es
an Ort und Stelle: die Knotenlinien stehen still, dazwischen schwingt die
Amplitude auf und ab — dieselbe Überlagerung zweier gegenläufiger Wellen, die eine
gezupfte Saite in Form hält. Die *Schwingungstiefe* bestimmt, wie weit das Feld
dabei zusammenfällt; bei 1 durchläuft es einen Moment völliger Ruhe.

**Raster** — Zehn Seitenverhältnisse vom Quadrat über 16:9 bis 9:16. Beim Wechsel
passt sich die Zeilenzahl automatisch an, damit die Zellen quadratisch bleiben und
das Bild randlos füllen; überschreiben kannst du sie danach jederzeit. Das
Wellenfeld selbst wird nie verzerrt — Kreise bleiben Kreise, das Format schneidet
nur einen anderen Ausschnitt heraus. Dazu Spalten, Zeilen und Helligkeitsstufen
(2 bis 30) frei wählbar; *Abstand* schafft Luft zwischen den Zellen, damit große
Bilder einander nicht überlagern.

**Bilder** — Standardmäßig aktiv. Die Slot-Anzahl folgt der Stufenzahl; Slot 1 ist
immer die dunkelste Stufe. Klick auf einen Slot öffnet die Bibliothek zur Auswahl.
**↕ Reihenfolge** dreht die Belegung um, falls die Bilder andersherum nummeriert
sind — die mitgelieferte `images.json` ordnet `solar-30` der dunkelsten und
`solar-1` der hellsten Stufe zu. Wer lieber Punkte sieht, schaltet *Bilder
verwenden* aus.

**Text** — Ein Wort zur Zeit erscheint im Raster. Das Wort wird in Rasterauflösung
gerastert; daraus entsteht ein Abstandsfeld, das für jede Zelle den Abstand zur
nächsten Buchstabenkante kennt — negativ innerhalb der Buchstaben. Dieses Feld
treibt eine eigene Welle, die Ringe laufen also buchstäblich von den Umrissen los
und überlagern sich mit dem Feld darunter.

Mehrere Wörter durch Leerzeichen trennen; sie wechseln im eingestellten Takt. Beim
Wechsel verschwinden nur die Buchstaben des alten Wortes — die von ihm bereits
ausgesandten Wellenfronten laufen weiter nach außen, während das neue Wort frische
Fronten von seinen eigenen Kanten aussendet. Möglich wird das, weil jede Front an
ihrer *Emissionszeit* geprüft wird, nicht am Jetzt: Eine Front weit draußen wurde
früher losgeschickt, als ihr Wort noch aktiv war, und bleibt deshalb bestehen.

*Stärke* regelt, wie sehr der Text das Feld überhaupt beeinflusst (0 schaltet ihn
ab), *Buchstabenfüllung* die Lesbarkeit. Die drei Kantenwellen-Regler sind
gitterunabhängig kalibriert: *Frequenz* (0,5–8) von einem breiten Schwung bis zu
dichten Ringen, *Reichweite* (0,05–1,5) von eng an den Buchstaben bis feldfüllend,
*Tempo* (0–3) wie schnell die Ringe nach außen wandern.

**Blende** — *Ausblenden* schickt von jeder Quelle eine letzte Wellenfront los: Sie
läuft nach außen, während die Helligkeit sinkt, und danach bleibt die dunkelste
Stufe stehen. Radiale Quellen senden Ringe, ebene Fronten eine wandernde Linie,
das Zentrum einen Ring um die Mitte. *Einblenden* dreht die Bewegung um. *Dauer*,
*Letzte Wellenfront* (Stärke) und *Lauf der Front* (Geschwindigkeit) sind
einstellbar; *Zurücksetzen* beendet die Blende.

Im Export gibt es dafür den Haken **Mit Ein- und Ausblendung**: Der Clip beginnt
dann schwarz, blendet auf und am Ende wieder ab. Die Blendendauer wird dabei auf
höchstens ein Drittel der Cliplänge gekürzt, damit vom Bild noch etwas übrig
bleibt. Mit der nahtlosen Schleife lässt sich das nicht kombinieren — ein Clip mit
Anfang und Ende ist keine Schleife —, deshalb sperren sich die beiden gegenseitig.

**Am Telefon** bleibt das Bild oben am Rand stehen, während die Regler darunter
scrollen — jede Änderung ist sofort sichtbar.

Seed und Phase bestimmen das Bild vollständig: dieselben Werte ergeben immer
exakt dasselbe Ergebnis.

**Teilen** — *↗ Link kopieren* legt den kompletten Zustand in die Adresse: Seed,
alle Parameter, Farben, Seitenverhältnis, Zeitpunkt und, falls abweichend, die
Slot-Belegung. Wer den Link öffnet, sieht dasselbe Bild — bei pausierter Animation
sogar pixelgenau denselben Frame. Was dem Standard entspricht, taucht im Link gar
nicht erst auf, deshalb bleiben die Adressen kurz (meist 100–150 Zeichen). *Code*
liefert dieselbe Zeichenkette ohne Adressteil, zum Einfügen in das Feld darunter.

---

## 6 · Export

Angegeben wird jeweils die **längste Kante**; die zweite Seite ergibt sich aus dem
gewählten Seitenverhältnis, auf gerade Pixelzahlen gerundet, weil Videoencoder
ungerade Maße nicht mögen.

**Einzelbild** — PNG bis 6000 px lange Kante.

**Video** — Auflösung, Format, Framezahl, Bildrate und Phasen-Schritt pro Frame.
Vier Formate:

| Format | Wann |
|---|---|
| **MP4 (H.264)** | Der Normalfall. Öffnet in Premiere, Final Cut, DaVinci, QuickTime. |
| **MOV (H.264)** | Derselbe Datenstrom, nur mit `.mov` benannt — für Programme, die auf der Endung bestehen. |
| **WebM (VP9)** | Für Web und als Rückfalloption. |
| **PNG-Sequenz (ZIP)** | Nummerierte Einzelbilder, verlustfrei, in jedem Schnittprogramm als Sequenz importierbar. Funktioniert immer. |

Ein Hinweis, der in der Praxis zählt: Manche Browser melden MP4 als unterstützt,
schreiben dann aber VP9 in den MP4-Container — eine Datei, die zwar `.mp4` heißt,
die Schnittprogramme aber nicht öffnen. Die Seite nimmt deshalb beim Laden drei
Testframes auf und liest im Container nach, was wirklich darin steckt. Kann der
Browser kein echtes H.264, sind MP4 und MOV in der Auswahl ausgegraut statt
stillschweigend kaputte Dateien zu liefern.

Stand heute liefern Chrome, Edge und Safari echtes H.264; Firefox kann es nicht —
dort sind WebM und die PNG-Sequenz die Wege.

**Geschwindigkeit** — Mit *Geschwindigkeit der Vorschau übernehmen* läuft die
Ausgabe genauso schnell wie das, was du auf dem Bildschirm siehst: Der
Phasen-Schritt je Frame wird aus dem Geschwindigkeitsregler und der gewählten
Bildrate berechnet, sodass bei 24, 30 oder 60 fps dieselbe Bewegung herauskommt.
Ausschalten gibt den manuellen Schritt-Regler frei.

Die Vorschau selbst rechnet dafür zeitbasiert statt bildbasiert — auf einem
120-Hz-Bildschirm lief sie vorher doppelt so schnell wie auf einem 60-Hz-Gerät.

**Nahtlose Schleife** — Damit ein Video ohne Sprung durchlaufen kann, muss das Feld
nach dem letzten Frame exakt wieder im Ausgangszustand sein. Von sich aus tut es
das nie: Jede Quelle läuft mit einer eigenen, zufälligen Rate, und deren gemeinsame
Periode ist praktisch unendlich.

Der Schalter rastet die Laufraten deshalb auf halbe Schritte ein. Damit gibt es eine
kürzeste Phasenlänge, nach der alle Generatoren wieder gleichzeitig am Anfang stehen
— je nach Seed meist eine oder zwei Einheiten. Aus dieser Länge und der
Vorschaugeschwindigkeit ergibt sich die Framezahl, die die Anzeige nennt; der
Frames-Regler tritt so lange zurück. Auch das Perlin-Rauschen wird schleifenfähig:
Statt geradeaus durch das Rauschfeld zu driften, läuft es auf einer Kreisbahn und
kommt nach einer Periode exakt am Ausgangspunkt an.

**Durchläufe** bestimmt, wie oft die Schleife hintereinander in der Datei liegt —
eins bis zwölf. Der Phasen-Schritt bleibt dabei unverändert, nur die Framezahl
vervielfacht sich; jede Nahtstelle im Inneren trifft exakt auf den Anfang. Nützlich,
wenn eine Plattform ein Mindestmaß an Länge verlangt oder das Video ohne eigene
Wiederholfunktion abgespielt wird.

Weil die Rasterung auch die Vorschau betrifft, siehst du die Schleifenbewegung
schon vor dem Export.

Das Video wird Frame für Frame gerendert und in Echtzeit aufgezeichnet. Unter Last
kann der Encoder einzelne Frames verwerfen — die Naht der Schleife bleibt davon
unberührt, weil alle Frames innerhalb einer Periode liegen; es entsteht höchstens
ein winziges Stocken. Kommt der Rechner gar nicht mit, wird die Datei länger als
vorgesehen und läuft damit langsamer als die Vorschau; die Statuszeile sagt es
dann. Wer es bildgenau braucht, nimmt die PNG-Sequenz — dort stimmt jeder Frame.
