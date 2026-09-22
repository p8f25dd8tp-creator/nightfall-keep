# NIGHTFALL KEEP

Ein browserbasiertes Mobile-Spiel. Du beginnst als **sterblicher Mensch** in einer verfallenen Burg
und steigst über das Blut deiner Feinde bis zum **Gottbezwinger** auf. Tagsüber (Dämmerung) baust du
deine Siedlung aus, nachts verteidigst du sie gegen die Jäger — Welle für Welle.

Das komplette Spiel steckt in einer einzigen Datei `index.html`: kein Build, keine Abhängigkeiten,
keine externen Bilddateien. Die gesamte Spielwelt wird zur Laufzeit auf Canvas gezeichnet.

## Starten

* **Lokal:** `index.html` im Browser öffnen, oder `npx http-server . -p 8080` und `http://localhost:8080` aufrufen.
* **Online:** Ein Push auf `main` veröffentlicht das Spiel über `.github/workflows/pages.yml` auf GitHub Pages.

## Der Aufstieg des Blutes

Jeder getötete Jäger gibt **Blut 🩸**. Blut wird niemals ausgegeben und geht nie verloren — es ist
dein dauerhafter Fortschritt über alle Partien hinweg. Bei jeder Schwelle steigst du einen Rang auf
und schaltest eine neue Fähigkeit frei:

| Rang | Blut | Fähigkeit |
|------|------|-----------|
| 🧍 Mensch | – | Sterblich — das Tageslicht macht dir nichts aus |
| 🩸 Halbvampir | 120 | **Lebensraub** — 10 % deines Schadens heilen dich. Ab hier schwächt dich die Sonne |
| 🦇 Vampir | 420 | **Nebelform** — jeder dritte Treffer geht durch dich hindurch |
| 👑 Vampiradliger | 1 150 | **Blutdiener** — eine Fledermaus kämpft dauerhaft an deiner Seite |
| 🏰 Vampirfürst | 2 600 | **Blutrausch** — volle Blutleiste löst 8 s doppelten Schaden und Tempo aus |
| ✨ Himmlischer | 5 400 | **Blutmond** — alle 9 s eine Blutnova; die Sonne wirkt nicht mehr |
| ⚡ Gottbezwinger | 10 500 | **Herrschaft** — alle Jäger in deiner Nähe verlieren 30 % Schaden und Tempo |

Mit dem Rang ändern sich **Aussehen und Werte des Helden** (Umhang, Kragen, Krone, Heiligenschein,
Aura, Blutklaue statt Schwert) und **die Burg selbst wächst mit**: verfallene Burg ➜ Vampirburg ➜
Blutzitadelle.

Zusätzlich vergibt jeder Stufenaufstieg im Kampf eine **Blutgabe** — ebenfalls dauerhaft
(Schattenklaue, Rasender Puls, Untotes Herz, Nebelschritt, Blutlanze, Gier).

## Bauen an festen Bauplätzen

Gebaut wird nicht frei, sondern an **16 festen Bauplätzen**, die von Anfang an im Gelände
abgesteckt sind (gestrichelte Raute mit 🔨). Vier davon liegen seitlich an jedem der drei
Angriffswege — sie tragen dessen Farbe —, der Rest ringt sich um die Burg.

* **Freien Bauplatz antippen** → Fenster mit allen fünf Gebäuden, Wirkung und Goldpreis. Auswählen baut sofort.
* **Gebäude antippen** → Ausbau-Fenster mit Werten und Kosten, bis Stufe 3.
* Fällt ein Gebäude, wird sein Bauplatz wieder frei.

Weil die Plätze fest sind, ist die Frage nicht *wohin*, sondern *was wohin*: ein Fledermausturm
am Weg, der heute Nacht angegriffen wird, ist viel wert — derselbe Turm am ruhigen Weg ist Gold
zum Fenster hinaus.

## Die Nacht: Wellen und Karten

Die Nacht dunkelt das Tal ein und färbt es violett, bleibt aber gut lesbar — Burg, Blutaltäre,
die Fackeln der Jäger und der Held werfen dabei warme Lichtinseln. Greifen Jäger den Bergfried an,
warnt ein großes rotes **DEINE BURG WIRD ANGEGRIFFEN!** über dem Spielfeld.

Jede Nacht besteht aus **3 bis 6 Wellen**, die letzte ist die **finale Welle** — sie wird
angekündigt und bringt ab Nacht 2 einen Inquisitor, in jeder dritten Nacht den Silberritter. Nach jeder überstandenen Welle wählst du **eine von drei
Karten**, die nur für diese Nacht gilt:

* **Zwei blaue Segen** — mehr Schaden, Gratis-Gebäude, Heilung, schwächere Jäger, Gold …
* **Eine rote Fluchkarte** — ein klarer Nachteil, dafür deutlich mehr Gold oder Blut
  (z. B. *Die Horde*: doppelt so viele Jäger, dafür doppeltes Gold und Blut).

Einmal pro Nacht kannst du die Karten neu ziehen.

## Die Angriffswege

Die Burg steht in der Nordwest-Ecke des Tals. Von den anderen Rändern führen drei optisch eindeutige
Wege zu ihrem Tor:

| Weg | Optik | Farbe |
|-----|-------|-------|
| ① Die Heerstraße | gepflasterte Straße mit Randsteinen | gold |
| ② Der Grabengang | ausgehobener Erdgraben mit Holzpfählen | blau |
| ③ Die Katakomben | dunkler Felstunnel mit Stützbögen | violett |

Wie viele Wege angegriffen werden, wächst mit der Nacht (1 → 2 → ab Nacht 4 alle drei). Welche Wege
**heute Nacht** aktiv sind, steht tagsüber in der Legende oben — danach richtest du deine
Verteidigung aus. An jedem Wegende steht eine Kapelle: von dort kommen die Jäger.

**Die Jäger:** Fackelträger (schnell, leuchten), Armbrustjäger (halten Abstand und schießen),
Inquisitoren (gepanzert, zäh) und der Silberritter als Boss in jeder dritten Nacht.

## Übersicht behalten

Weil die Kamera weit herausgezoomt ist, gibt es zwei Orientierungshilfen:

* **Gegnerzähler** in der Kopfzeile: `NACHT 8 · WELLE 2/4 · 7 ⚔`
* **Minimap** oben rechts: zeigt das ganze Tal mit allen drei Wegen (aktive Wege leuchten), Burg,
  eigenen Gebäuden, Blutteich, deinem Helden und dem aktuellen Bildausschnitt. Antippen klappt sie
  auf ein kleines 🗺-Symbol zusammen.
* **Richtungs-Pins am Bildrand** mit Entfernung in Metern — je ein Pin pro Angriffsweg, auf dem
  gerade Jäger unterwegs sind, plus einer zur Burg.

## Steuerung

* **Linker Daumen** (unten links) oder **WASD / Pfeiltasten**: Held bewegen
* Held, Fledermaustürme, Blutaltäre und die **Wachen auf der Burgmauer** greifen automatisch an
* **Bauen und Ausbauen:** Bauplatz oder Gebäude antippen (siehe oben). Ein Tipp neben das
  geöffnete Fenster schließt es wieder.
* **Rangleiste oben links** oder **📜**: Heldenwerte, alle Ränge, Blutgaben und die Regeln
* **🔍**: Zoomstufe · **×1 / ×2 / ×3**: Geschwindigkeit · **Leertaste**: Nacht starten · **Esc**: Bauen abbrechen

## Regeln

**Gold 🪙 baut, Blut 🩸 steigt auf.** Beides sind getrennte Ressourcen:

* Gebäude kosten Gold: Knochenwall 25 · Dienerhütte 35 · Blutaltar 45 · Fledermausturm 60 · Blutquelle 80
* **Dienerhütte** (+0,9 🪙/s) und **Blutquelle** (+2,2 🪙/s) erzeugen laufend Gold — in der Dämmerung
  voll, nachts zu 40 %. Jede Ausbaustufe vervielfacht die Ausbeute.
* **Goldadern ⛏** im Gelände: in der Dämmerung den Helden danebenstellen, nach kurzer Zeit 18 🪙.
  Jeden Morgen erscheinen neue.
* **Blut gibt es ausschließlich aus besiegten Jägern** (3–44 🩸, steigend mit der Nacht).
* Gebaut wird im Ring um die Burg — nicht auf den Angriffswegen und nicht im Blutteich.

## Speicherung

| Schlüssel | Inhalt | Verhalten |
|---|---|---|
| `nightfall-meta-v3` | Rang, Blut, Blutgaben, Statistik | **Dauerhaft** — überlebt Niederlage, Neustart und Browser-Neustart |
| `nightfall-run-v3` | Nacht, Gold, Gebäude, Lebenspunkte | Die laufende Partie, über *FORTSETZEN* weiterspielbar |

*NEUE PARTIE* verwirft nur die Partie, niemals Rang oder Blutgaben.

## Technik

* Vanilla JavaScript, Canvas 2D, keine Frameworks und keine Bilddateien.
* Das Gelände (Gras, Gräber, Wege, Blutteich, Felsrand, Burghof) wird beim Start **einmalig** in eine
  Offscreen-Canvas gerendert und danach nur noch als Bild gezeichnet — das hält die Bildrate auch auf
  dem Handy bei ~60 fps.
* Nachtbeleuchtung über eine separate, halb aufgelöste Licht-Canvas mit `destination-out`-Lichtkegeln
  für Burg, Held, Blutaltäre, Fenster und die Fackeln der Jäger.
* Die Bedienelemente liegen in getrennten, überschneidungsfreien Zonen (Joystick links unten,
  Bau-Leiste am unteren Rand, Aktionen rechts darüber); Tippen auf die Karte wird nur ausgewertet,
  wenn kein Bedienelement getroffen wurde. Geprüft von 320 px bis 1440 px und im Querformat.
