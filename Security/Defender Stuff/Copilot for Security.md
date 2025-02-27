## Beschreibung
Copilot for Security ist ein Tool welches erlaubt, mit Hilfe von Copilot Informationen durch KI anzureichern. Ausserdem kann man sich Code (beispielsweise Powershell oder[[KQL (Syntax)|KQL]]) generieren lassen, um zusätzliche [[Azure Sentinel#Hunting|Huntings]] zu starten. Wenn man innerhalb vom [[Unified Security Portal]] einen Alert hat, kann man dabei direkt auf den Copilot for Security zugreifen. Folgend eine Übersicht der Funktionsweise:
![[funktionsweise copilot for security.png]]
Microsoft gibt auf dem Dashboard von Copilot for Security Tipps, wie man Incidents anreichern/lösen kann.
## Berechtigungen
Siehe [[Berechtigungen#Copilot for Security Rollen]]

## Promptbooks
#### Beschreibung
Promptbooks sind wie [[Azure Sentinel#Analytic Rules|Analytic Rules]], jedoch in Form von sprachlichem Text. In einem Promptbook stehen Anweisungen/Fragen, welche anschliessend von der Copilot-Engine ausgeführt werden (siehe Abbildung oben). In einem Promptbook können mehrere Anweisungen (Prompts) auf **einmal** stehen. Diese werden anschliessend nacheinander ausgeführt.
Microsoft gibt standardmässig bereits Promptbooks mit, welche 1:1 ausgeführt werden können.
#### Erstellen eines Custom-Promptbooks
Ein Promptbook kann erstellt werden, in dem man einen bereits existierenden Prompt (in der Prompt-Eingabe) als Promptbook speichert.
Anschliessend kann man folgendes konfigurieren:
- Name des Promptbooks
- Tags
- Description
- Prompts
- Variabeln
- Wer das Promptbook alles sehen darf
#### Variablen (Inputs)
Innerhalb eines Promptbooks können auch Inputs in Form von Variablen mitgegeben werden. Diese werden durch "<>" mitgegeben. 
Falls man beispielsweise ein Script analysieren möchte, kann man dies mit einem Prompt + \<SCRIPT> machen. Anschliessend, wenn man das Promptbook aufruft wird man gebeten, das Script als Input zu definieren.
## Quellen und Plugins
#### Standardquellen - und Plugins
Copilot for Security reichert Daten per Default von folgenden Quellen an:
- [[EntraID]]
- [[Intune]]
- [[Purview]]
- [[Azure Sentinel]]
- [[Defender for Endpoint]]
#### Erweiterte Quellen
Copilot for Security kann auch noch weitere Daten ingesten. Beispiele hierfür sind
- Eigene Fileuploads (bsp. Playbooks)
- Subscription Data (bsp. Intune Data oder anderweilige Azure Policies)
- Third Party Plugins (andere Logquellen oder z.B. AbuseIPDB usw.. (siehe [hier](https://learn.microsoft.com/en-us/copilot/security/plugin-overview)))

## Connectors
Mit Connector ist ein spezieller Wrapper um die Copilot for Security [[API]] gemeint welcher Entwickler erlaubt, spezielle Aufgaben ausserhalb von Copilot auszuführen. Momentan sind folgende Connector unterstützt:
- Logic Apps Connector (zum Ausführen von Logic Apps)
- Power Automate (andere Form von Logic Apps)