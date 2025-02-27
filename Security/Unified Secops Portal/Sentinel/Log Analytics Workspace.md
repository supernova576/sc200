## Beschreibung
Ein "Bucket", welches Logs standardisiert (siehe [[KQL (Syntax)#Tables]]) collected. [[Azure Sentinel]] läuft auf einem Log Analytics Workspace. Logs kann man mittels KQL abfragen.
## Linux Test Alert
Um Logs von einer Linux Maschine zum Log analytics workspace zu bringen, müssen folgende Schritte gemacht werden:
1. Azure Defender auf die Subscription berechtigen
2. Kopieren irgendeines (spielt keine Rolle) Executables auf die Linuxmaschine
3. Executable "**ASC_AlertTest_662jfi039N.exe**" (wtf..) nennen
## Daten von einer anderen Cloud importieren
Beispiel mit Google Cloud: 
![[log_analy_google_cloud.png]]

## Send SYSLOG to Log Analytics Workspace
Um SYSLOG Logs zu senden, werden folgende Parameter für den Log Analytics Workspace gebraucht:
1. Ressource Group 
2. Sekundärer Key