## Allgemeines / Alerting
MDE läuft direkt auf dem Gerät (Endpoint). MDE agiert wie ein Antivirusprogramm, welches Alerts und Daten direkt an das Unified Security Portal senden kann.
#### Suppression Rules
Falls man eine Gruppe von Leuten / Devices hat (bsp. **Developer**, **Trader**) welche spezielle Applikationen brauchen, kann man eine Exception für Alerts einrichten. Die Alerts werden dabei **noch immer** generiert, jedoch anschliessend versteckt.
#### Detection Rules
Detection Rules sind abgespeicherte Advanced Hunting Queries ([[Azure Sentinel#Advanced Hunting Query]]), welche direkt auf dem MDE laufen.

## Attack Surface Reduction (ASR)
Attack Surface Reduction Rules sind unterteilt in zwei Kategorien:
- Standard Protection Rules (minimale von Microsoft empfohlene Konfiguration, offizielle ASR Rules, sind bereits out-of-the-box erhältlich)
- Other (alle übrigen)
Eine detaillierte Liste gibt es [hier](https://learn.microsoft.com/en-us/defender-endpoint/attack-surface-reduction-rules-reference?view=o365-worldwide).
#### Beispielsanwendung
Beispielsweise können mittels ASR-Rules Excel oder Word Makros durch verbieten von Subprozessen geblockt werden. 

## Erweiterte Features
Erweiterte Features können direkt im Defender-Portal in den Einstellungen konfiguriert werden.
#### Live Response (Client und Server)
Live Response ermöglicht es dem Analyst, **direkt** auf einen betroffenen Host zu verbinden. Folgende Kommandos sind hierbei direkt aus der Shell aufrufbar:

| Command        | Nutzen                                                                 |
| -------------- | ---------------------------------------------------------------------- |
| cd             | Change Directory                                                       |
| connections    | Zeigt alle aktuellen Verbindungen an                                   |
| drivers        | Listet alle installierten Treiber auf                                  |
| fileinfo       | Gibt alle Informationen über ein File an                               |
| findfile       | Sucht nach einem File                                                  |
| getfile        | Ladet sich ein File herunter.                                          |
| processes      | Listet alle Prozesse auf                                               |
| scheduledtasks | Listet alle scheduled Task auf.                                        |
| analyze        | Analysiert den Host und gibt anschliessend ein Verdikt aus             |
| putfile        | Ladet ein File hoch                                                    |
| remediate      | Löscht, Stoppt, Terminiert Sachen (Prozesse, Files, Verbindungen, ...) |
| scan           | Schnellscan gegen Malware                                              |
| undo           | Restores a remediated entity                                           |
#### EDR im Block-Modus
EDR ist per Default im "Alert"-Modus. Falls EDR in den Block-Modus geschaltet wird, werden suspekte Aktivitäten direkt geblockt (**keine** Benachrichtigungen mehr!!).
#### Allow or Block Files
Folgende Voraussetzungen müssen vor dem Aktivieren des Features erfüllt sein:
1. MDE ist der **Hauptantivirus**
2. Cloud Based Protection ist aktiviert.
Wenn das Feature eingeschaltet ist, werden maliziöse Files automatisch geblockt (kein read, kein write, kein execute).
#### Hide potential duplicate device records
Wenn dieses Feature aktiv ist werden Duplikate, welche "älter" sind, vom Device Inventory **versteckt**.
#### Tamper protection
Beim Aktivieren dieses Features werden sämtliche Versuche, den MDE Antivirus auszuschalten (von bsp. Apps oder Methoden oder automatisierten Actions), unterdrückt.
#### Device Discovery
Scannt nach unmanaged Devices (diese können anschliessend Contained werden).
#### Herunterladen von Quarantänisierten Files
Selbsterklärend.
#### Deception
Siehe [[Defender XDR#Deception Role]]

## Device Management
#### Device Groups
Device Groups sind Gruppen von Endgeräten, die sich in einer logischen Einheit befinden.
#### Hunting mit Device Groups
Um beispielsweise Automatisierungen von **mehreren** Device Groups wahrzunehmen (bsp. Zusammenhang mit [[Azure Sentinel#Advanced Hunting Query]]), können bereits bestehende Device Groups durch **Tagging** zusammengeführt werden:
1. Tag auf Device Group Ebene hinzufügen
2. Tag auf betroffene Maschinen hinzufügen
3. Neue Device Group erstellen (mit Rank 1!!)
#### Contain vs. Isolate

| Contain                                                                | Isolate                                                                |
| ---------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| Bei **ungemanagten** Devices                                           | Nur bei **gemanagten** Devices                                         |
| Sagt allen **gejointen** Devices, nicht mehr mit diesem Host zu reden. | Isoliert den Host vom Netzwerk, damit er keine Daten mehr senden kann. |

## Risk Rating
MDE erstellt von jedem Endpoint ein Risk Rating, welches basierend auf Vulnerabilities, kürzlichen Events und vergangenen Events kreiert wird. Bei einer Infizierung durch Malware wird das Risk Rating beispielsweise automatisch angepasst.

## Vulnerability Scanning
MDE bietet die Möglichkeit, den Endpoint direkt auf Vulnerabilities zu scannen. Erkannte Vulnerabilities werden als Alert angezeigt.




