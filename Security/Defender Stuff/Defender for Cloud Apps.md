## Beschreibung
Defender for Cloud Apps spezialisiert sich auf third-party SaaS-**Apps** , welche nicht von Microsoft direkt kommen, aber auf Azure laufen.
## Discovered Apps
Hier befinden sich alle Applikationen, welche registriert wurden. Es ist ein "Submodul" von [[Defender for Endpoint]] und [[Defender XDR]]
#### Sanctioned
Sanctioned Apps sind **approved** und somit von der Organisation **akzeptiert**.
#### Unsanctioned
Unsanctionied Apps sind **nicht approved** und somit von der Organisation **nicht akzeptiert**.
Ohne den Defender for Endpoint muss zuerst ein Blockscript installiert werden, um den Traffic von unsanctioned Apps zu blockieren. Hierfür ist nötig:
1. App selektieren
2. App als unsanctioned markieren
3. Generieren vom Blockscript
4. Ausführen des Scripts auf der **Source Appliance**

## External Sharing of Files
#### automatischer Alert und Remediation
Um einen solchen Alert einzurichten, muss man über AIP (Azure Information Protection) gehen. Folgende Parameter müssen dabei aktiviert werden:
- Azure Information Protection => automatically scan new files for classification lables
- **Enable File Monitoring**

## Policies für Cloud App
Policies, welche mehr als:
- 200 000 Matches pro Tag
- 100 000 Matches pro 3 Stunden
haben, werden in der Regel automatisch disabled.
#### Access Policy
Besagt, wer wohin verbinden darf (ähnlich wie eine Firewall). Die **Zugriffsdaten** basieren auf Benutzer, Lokation, Device usw. 
#### Activity Policy
Suspekte Aktivitäten, welche meistens eine Art **Interaktion** benötigen, wie beispielsweise das Herunterladen von 1000 Files innerhalb von 15 Minuten oder 50 fehlgeschlagene Loginversuche hintereinander. 
#### Anomaly Detection Policy
Out of the Box Lösungen, welche durch [[Defender XDR#UEBA Policies]] geprägt sind. Anomalien können beispielsweise:
- Risky IP Address
- Impossible travel
- Activity Rate
- Detection of [[Botnets]] 
usw sein.
#### Session Policies
Realtime Session Policies, beispielsweise zur Überwachung mittels [[DLP]].
#### File Policies
File Policies umschreiben Alerts wie zum Beispiel DLP, Compliance Scans oder AIP.
Defender for Cloud Apps kann jeden Dateityp auf der Grundlage von mehr als 20 Metadatenfiltern wie Zugriffsebene, Dateityp und **trainable classifiers** überwachen

