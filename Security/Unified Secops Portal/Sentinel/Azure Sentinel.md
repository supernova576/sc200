## Beschreibung
Software, welche auf einem [[Log Analytics Workspace]] läuft und zusätzliche Informationen / Automatiserungsmöglichkeiten liefert (SIEM und SOAR in einem). Die maximale Incident-Aufbewahrung beträgt 30 Tage.

## Named Location
Named Locations sind eine Zusammenkunft aus meheren (oder einzelnen) **Netzerken**. Beispielsweise könnte man hier mehrere IPv4 sowie IPv6 Adressen angeben und diese anschliessend einer logischen Einheit zusammenführen.
##### Gruppierung nach Land
Durch die IPv4-Adress-Ranges könnte man auch mit einem Filter pro Land setzen

## Hunting
Falls man einem Alert mehr nachgehen will, kann man einen "Hunt erstellen". Dieser besteht aus einer eigens-gebastelten [[KQL (Syntax)]]-Abfrage, welche zusätzliche Daten enricht. "Hunts" werden als **separate Entität** behandelt, man kann sie also jeder Zeit bearbeiten.
#### Als Favoriten speichern (Autorun Query)
Wenn man einen Hunting-Query als Favoriten speichert, läuft der Hunting Query **jedes mal**, wenn man den Blade neu öffnet.
#### Bookmarking (Queries speichern)
Wenn man einem Query ein Bookmark hinzufügt, werden alle vergangenen Queries (inkl. Resultaten) gespeichert.
#### Advanced Hunting Query
Advanced Hunting Queries sind bereits vordefinierte (durch Content Hub installierte) oder selbstständig erstellte KQL-Queries.
#### Live Streams
Live Streams ist nichts anderes, als real-time-analytict innert der Hunting Query. (ähnlich wie bei Linux tail -f). Nur Hunting Queries können Live Streams zugezogen werden.

## Watchlist
Eine Watchlist ist ein "custom" Table, welches man zum Enrichen von zusätzlichen Daten brauchen kann. Der Import funktioniert über CSV.

## Analytic Rules
#### Beschreibung
Analytic Rules sind nichts anderes als KQL-Queries, welche periodisch laufen. Dabei unterscheidet man zwischen 
- Near Real Time (NRT)
- Scheduled (periodisch)
#### Types von Analytic Rules
Bei Analytic Rules unterscheidet man zwischen mehreren Untergruppen. Diese sind folgend beschrieben:

| Type                    | Beschreibung                                                                                                                                                                                                       |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Scheduled               | Normale KQL-Analytic Rules, welche periodisch ausgeführt werden. Benutzt **Entity mapping**.                                                                                                                       |
| Anomaly                 | "Informational (Dringlichkeit)" und identifizieren "anomalische" Ereignisse. Werden im "Anomalies"-Table im [[Log Analytics Workspace]] gespeichert. **GENERIERT KEINE ALERTS**. Diese haben einen Score von 0-10. |
| Fusion                  | Korreliert mehrere Alerts und stellt mittels ML einen "multistage" Alert zusammen. Können (wie ML behavioral Analytics) nicht reviewed werden.                                                                     |
| Microsoft Security      | Automatisches Alertgenerating durch Microsoft Apps (Defender for X, usw.)                                                                                                                                          |
| ML behavioral Analytics | Können nicht editiert oder modifiziert werden. Sentinel built-in. Ähnlich wie Fusion.                                                                                                                              |
#### Investigation mit Sentinel
Von den oben genannten Types können nur Scheduled und NRT-Rules investigated werden.

## Mehrere Sentinel-Instanzen (Sentinelesen?)
Wenn man mehrere Sentinel Workspaces auf einmal einsieht, sieht man nur den "Incidents"-Tab. Für weitere Actions muss man wieder in die Einzelansicht wechseln.

## Logic Apps (Playbooks)

#### Diagnostics
Um Fehler bei Logic Apps auswerten zu können, **muss** unter Playbook Diagnostics der Log-Analytics-Workspace angegeben werden. Ansonsten werden Fehler defaultmässig nicht geloggt.
#### Nutzung
Playbooks führen automatisierte Actions aus, welche aktiv in den laufenden Betrieb eingreifen.
#### Konfiguration
Playbooks können im **Logic App Designer** konzipiert werden. Wichtig beim Erstellen eines Playbooks ist, dass das Playbook die nötigen Berechtigungen hat, um in eine Umgebung einzugreifen.

## Automation Rules
Automation Rules sind die **Trigger**, welche anhand von Kriterien Actions an einem Incident vornehmen. Beispiele sind:
- Autoclose Incident
- Run Playbook
- Assign Tag
- Add Comment
## Content-Hub
Im Content-Hub können Erweiterungen/Integrations für hauseigene oder  third-party Applikationen gefunden werden.
Innerhalb eines Packetes können sich folgende "Artikel" befinden:
- Analytic Rules
- Workbooks
- Data Connector inkl. [[KQL (Syntax)#ASIM Parser|ASIM-Parser]]

## Data Collection Rules
Data Collection Rules sind "Ingestion"-Regeln, welche bestimmen, welche Daten in den [[Log Analytics Workspace]] von Sentinel kommen und welche nicht.
#### Exkludieren von Data-Columns
1. Data Connector auswählen und in die Einstellungen navigieren
2. Data Collection Rule hinzufügen (**nicht** bei allen Connectoren unterstützt!!)
Anschliessend können Log-Ingestions durch folgenden KQL-Command **exkludiert** werden:
```kql
source |
project-away <column-name>
```

## Data Connectors
Data Connectors sind virtuelle "Listener", welche Daten 
1. aufnehmen
2. parsen (falls ein [[KQL (Syntax)#Parsers|Parser]] und eine Data-Collection Rule vorhanden ist)
3. ingesten (ins System laden)
Data Connectors von grossen Applikationen (Splunk, ...) können vom Content-Hub installiert werden.
Data Connectors können aber auch von Grund auf selbst konfiguriert werden. Dabei spielt die [[Azure Sentinel#Data Collection Rules|Data Collection Rule]] eine wichtige Rolle.
Falls man die Logs anschliessend normalisieren möchte, kann man einen eigenen Parser dazu schreiben.
#### Entity Ingestion
Sämtliche Entitäten werden über Data Connectors aufgenommen. Beispielsweise können User-Daten durch den [[Defender for Identity]]-Connector aufgenommen werden. 
#### WEF und WEC
WEF steht für Windows Event Forwarding. Scope dieser Logs sind alle betriebsbezogenen sowie administrativen Daten. Ein System kann so konfiguriert werden, dass die Logs entweder **gepusht** oder **gepullt** werden. *WEF-Logs* werden anschliessend an einen ***WEC-Server*** (Windows Event Collector) gesendet.
## Workbooks
Workbooks sind Dashboards, welche Daten anzeigen. Sie können selbst konfiguriert werden oder im Content-Hub heruntergeladen werden.