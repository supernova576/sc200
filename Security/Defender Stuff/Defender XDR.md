## Beschreibung
XDR steht für **Extended Detection and Response**. Es ist eine Suite (Zusammenfassung) bestehend aus mehren Produkten. Ziel von XDR ist es, eine Komplettlösung für den SOC-Betrieb zu bieten.
## Umfassung Defender for XDR
Die Suite besteht aus vier Hauptkomponenten:
1. [[Defender for Office 365]]
2. [[Defender for Identity]]
3. [[Defender for Cloud Apps]]
4. [[Defender for Endpoint]]
5. [[Defender for Cloud]]
## Tier-System
Folgende Tiers werden unterschieden:

| Tier | Beschreibung                                                                                                                     | Titel         |
| ---- | -------------------------------------------------------------------------------------------------------------------------------- | ------------- |
| 0    | Vollständige Automation von alltäglichen Alerts                                                                                  | Automation    |
| 1    | Tier1 bekommt malware alert und erkennt, dass es sich um evtl. mehr aufwand handeln könnte und leitet den Alert an Tier2 weiter. | Triage        |
| 2    | Tier2 nimmt alle nötigen Steps auf sich und schliesst anschliessend den Alert.                                                   | Investigation |
| 3    | Tier3 sieht den geschlossenen Alert und schaut sich das nochmals an und macht den Feinschliff.                                   | Hunt          |

## UEBA Policies
[[UEBA]] (User Entity and Behavior Analytics) ist ein Modul welches Daten von Benutzern analysiert und anhand von speziellen Policies Entscheidungen fällt. Log-Quellen, welche von UEBA benutzt werden sind:
- **AzureActivity**
- **SecurityEvents**
#### Impossible Travel
In dieser Policy werden der **neueste Login** und der **letzte Login vor dem neuesten Login** miteinander verglichen. Defender XDR hat also bereits **schonmal einen Login geloggt**. Falls sich also jemand innerhalb von 5 Minuten einmal von den USA und einmal von China angemeldet hat, schlägt diese Policy an.
###### False Positive Tuning
Um legitime IP-Adressen vom Alerting des Impossible Travel zu lösen, wird ein whitelist-Ansatz empfohlen. Zuerst sollte man das **Data Enrichment**-Feature aktivieren um anschliessend die enrichten IP-Adressen in die **Range der Organisation** hinzuzufügen, um weitere Alerts vorzubeugen.
#### Activity from infrequent country
Hier werden alle "normalen" Logins beobachtet. Falls also jemand von einem Land einloggt, welches zuvor noch keinen Login erfahren hat, schlägt die Policy an. Dies kann beim **ersten** oder **willkürlichen** Login passieren.
#### Malware detected
Schlägt an, wenn Daten von der [[Threat Intelligence Platform]] als malicious geflaggt werden.
#### Deception Role
Deception (Täuschungs-) Roles erstellen beim Erkennen von Lateral Movement, BEC, Malware, ... mehrere [[Honeypots (-tokens)]] Accounts, welche an spezifische Endpunkte automatisch ausgerollt werden. Falls der Angreifer nun einen solchen Account versucht zu hacken, ensteht ein Alert.

## Automated Investigation and Response (AIR)
Automatische Investigation und Response von Alerts. 
Falls der Antivirus auf "passiv" gestellt wird, werden die Alerts **nicht** komplett automatisch abgehandelt, sondern geben lediglich **Empfehlungen** zur Lösung des Problems. Um AIR verwenden zu können, müssen folgende Voraussetzungen erfüllt sein:
- MDE aktiviert
- MD for Cloud Apps konfiguriert
- MD for Identity Connector
#### Self-Heal
Self-Heal ist ein Feature, welches automatisch die gleichen Schritte wie ein Analyst veranlasst, um Incidents zu
- Analysieren
- Kategorisieren
- Lösen
AIR kann einfache automatisierte Handlungen für folgende Defender abhandeln:
- MDE (Isolation, Sperrung, ...)
- MD for Office 365 (Links blokieren, Emails quarantänisieren, ...)
- MD for Identity (Acocunts temporär sperren, Sessions revozieren, ...)