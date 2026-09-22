# NIGHTFALL KEEP

Ein browserbasiertes Mobile-Spiel: **tagsüber die Festung ausbauen, nachts die Angriffswege verteidigen.**
Das komplette Spiel steckt in einer einzigen Datei `index.html` — kein Build, keine Abhängigkeiten,
keine externen Assets. Die gesamte Spielwelt wird zur Laufzeit auf Canvas gezeichnet.

## Starten

* **Lokal:** `index.html` im Browser öffnen (Doppelklick genügt), oder
  `npx http-server . -p 8080` und dann `http://localhost:8080` aufrufen.
* **Online:** Ein Push auf `main` veröffentlicht das Spiel über den Workflow
  `.github/workflows/pages.yml` auf GitHub Pages.

## Die Welt

Das Tal misst 2100 × 1750 Einheiten und ist von einer Felswand umschlossen. Die eigene **Festung
steht in der Nordwest-Ecke**; von den übrigen Rändern führen **drei klar unterscheidbare Angriffswege**
zum Tor:

| Weg | Optik | Farbe |
|-----|-------|-------|
| ① Steinstraße | gepflasterte Straße mit Randsteinen und Kies | gold |
| ② Der Graben | ausgehobener Erdgraben mit Holzpfählen | blau |
| ③ Schattentunnel | dunkler Felstunnel mit Stützbögen | violett |

Wie viele Wege angegriffen werden, wächst mit der Nacht: Nacht 1 → ein Weg, Nacht 2–3 → zwei Wege,
ab Nacht 4 → alle drei. Welche Wege **heute Nacht** aktiv sind, steht tagsüber in der Weg-Legende
oben und über den Markierungen im Gelände — danach lohnt es sich, die Verteidigung auszurichten.

## Steuerung

* **Linker Daumen** (unten links) oder **WASD / Pfeiltasten**: Held bewegen
* Held, Wachtürme, Feuerstellen und die **Wachen auf der Festungsmauer** greifen automatisch an
* **Bauen:** unten ein Gebäude wählen → auf die Karte tippen, um die Vorschau zu setzen → **✓** bestätigen
  (grün = Platz frei, rot = Grund steht daneben). **✕** bricht ab.
* **Aufwerten:** ein bestehendes Gebäude antippen → Infofenster mit Werten und Kosten → *AUFWERTEN* (bis Stufe 3)
* **🛡️** oben rechts: Heldenwerte, dauerhafte Verbesserungen und die Spielregeln
* **🔍**: Zoomstufe umschalten (SEHR FERN / FERN / NAH)
* **×1 / ×2 / ×3**: Spielgeschwindigkeit · **Leertaste**: Nacht starten · **Esc**: Bauen abbrechen

## Regeln

**Gold ist die einzige Ressource.** Es gibt vier Quellen:

1. **Häuser** (+0,9 🪙/s) und **Mühlen** (+2,2 🪙/s) erzeugen laufend Gold — tagsüber voll, nachts 40 %.
   Jede Ausbaustufe vervielfacht die Ausbeute.
2. **Goldadern** ⛏ im Gelände: tagsüber den Helden danebenstellen, nach kurzer Zeit gibt es 18 🪙.
   Jeden Morgen erscheinen neue.
3. **Besiegte Gegner** lassen nachts Gold fallen (Schatten 7, Brocken 14, Boss 60 — steigend mit der Nacht).
4. Die dauerhafte Verbesserung *Glückssträhne* erhöht alle Goldeinnahmen.

**Gebäude kosten Gold:** Palisade 25 · Haus 35 · Feuerstelle 45 · Wachturm 60 · Mühle 80.
Gebaut wird im Ring um den Bergfried, nicht auf den Angriffswegen, nicht im Wasser.

## Dauerhafte Helden-Verbesserungen

Jeder Stufenaufstieg im Kampf lässt eine von sechs Verbesserungen wählen
(Schaden, Angriffstempo, Leben, Tempo, Reichweite, Gold). Diese Ränge werden **getrennt von der
laufenden Partie** unter `localStorage["nightfall-meta-v2"]` gespeichert und bleiben nach einer
Niederlage, einem Neustart und dem Schließen des Browsers erhalten. Der Startbildschirm und das
🛡️-Panel zeigen jederzeit den aktuellen Stand.

Die laufende Partie (Nacht, Gold, Gebäude, Lebenspunkte) liegt getrennt davon unter
`localStorage["nightfall-run-v2"]` und lässt sich über *FORTSETZEN* weiterspielen;
*NEUES SPIEL* verwirft nur die Partie, niemals die dauerhaften Verbesserungen.

## Technik

* Vanilla JavaScript, Canvas 2D, keine Frameworks und keine Bilddateien.
* Das Gelände (Gras, Blumen, Wege, See, Felsrand, Burghof) wird beim Start **einmalig** in eine
  Offscreen-Canvas gerendert und danach nur noch als Bild gezeichnet — das hält die Bildrate
  auch auf dem Handy bei ~60 fps.
* Nachtbeleuchtung über eine separate, halb aufgelöste Licht-Canvas mit `destination-out`-Lichtkegeln
  für Bergfried, Held, Feuerstellen und Fenster.
* Die Bedienelemente liegen in getrennten, überschneidungsfreien Zonen (Joystick links unten,
  Bau-Leiste am unteren Rand, Aktionen rechts darüber); Tippen auf die Karte wird nur ausgewertet,
  wenn kein Bedienelement getroffen wurde.
