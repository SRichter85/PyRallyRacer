# PyRallyRacer

## Beschreibung

PyRallyRacer ist ein 2d-Topdown Rennspiel welches mit Python entwickelt wird.

Der Spieler steuert dabei ein Auto durch eine Strecke und versucht seine eigene Bestzeit zu schlagen. Die Hauptfeatures sind:

- Graphische 2D Darstellung eines Autos und Rennstrecke
- Das Auto wird physikalisch modelleriert: Lenken lenkt nur Reifen, Gas erhöht Drehmoment, Bremsen verringert Drehzahl. Die eigentliche Kraft auf das Auto wird dann errechnet.
- Strecken können mit MSPaint gezeichnet werden.

Zukünftige Features:

- Ghostcars
- Strecken können verbunden werden, um "Etappen" zu simulieren (und um grosse Strecken zu erstellen)
- Mehrere unterschiedliche Autos
- Weitere physikalische Effekte (Aufhängung, etc.)

## Physikalische Berechnung

**Beschleunigung:** der Benutzer beschleunigt nicht das Auto direkt sondern er gibt "Gas", welches die Drehzahl des Motors erhöht wodurch ein Drehmoment auf den Reifen erzeugt wird, welcher dann in eine Kraft umgewandelt wird. Zusammen mit den Friktionskraft (Reifen zu Untegrund, Rollwiderstand) und dem Luftwiderstand wird die Gesamtbeschleunigung des Autos errechnet.

Wichtig: Bei einem normalen Auto können, wenn man maximal Gas gibt, die Reifen durchdrehen. Hier werden wir ein Mechanismus haben. Da Input binär ist, brauchen wir dafür einen Input

**Bremsen:** Der Benutzer betätigt Bremse durch Keyboard. Um Komplikationen zu vermeiden, gibt es nur zwei Arten von Bremsen:
- normale Bremse mit ABS, d.h. maximale Bremskraft bevor die Reifen blockieren
- Handbremse, d.h. maximale Bremskraft selbst wenn die Reifen blockieren

**Lenken:** Der Benutzer ändert durch einen Lenker die Richtung der Vorderreifen. Die Bewegungsrichtung wird errechnet basierend auf Rollwiderstadt und Oberflächenwiderstand. Dadurch kann das Auto "driften".

**Gewichtsverteilung** Noch nicht sicher ob wir das brauchen. Aber beim Beschleunigen/Bremsen verlagert sich das Gewicht, wodurch gewisse Widerstandskräfte sich ändern können.

## Karten Generation
Der Benutzer kann eigene Karten zeichnen mit MSPaint. Aus dem gezeichneten Bild wird dann eine Rennstrecke ('Track') erzeugt. Es werden folgende Konventionen vereinbart: 1 Pixel im Bild entspricht 1m in Spielkoordinaten. Für die unterschiedlichen Objekte und Fahruntergründe gibt es folgende Farbcodes:

|RGB|Objekt/Oberfläche|
|--|--|
|0, 255, 0|Grass|
|128,128,128|Asphalt|
|255,255,255|Startzone|
|255,255,0|Checkpoint|
|255,0,0|Zielzone|