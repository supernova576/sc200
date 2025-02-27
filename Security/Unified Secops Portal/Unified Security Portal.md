## Beschreibung
Plattform (security.microsoft.com), welche Alerts sowie Konfigurationsmöglichkeiten von folgenden Apps bietet / anzeigt:
- [[Defender XDR]] (inkl. alle Sub-Defender)
- [[Azure Sentinel]]
- [[Defender for Cloud]]
- [[Copilot for Security]]
## Benötigte Rechte
Um auf das Unified Sec Portal zu kommen, benötigt man mindestens 2 Rollen (Least Privilege)
1. Active Remediation Action Role für MDE
2. Security Reader für Azure AD
## Konfigurationen
#### Konfigurieren von Benachrichtigungen
Benachrichtigungen können direkt im Defender Portal unter "Einstellungen > Endpoints > Allgemein > Email".
Anschliessend kann eine neue Regel zum Benachrichtigen erstellt werden. Hier entscheidet man, ob man über einzelne [[Defender for Endpoint#Device Groups|Device Groups]] oder über alle Geräte hinweg (benötigt Security Administrator-Rechte) benachrichtigt werden möchte.

## Exposuremanagement
Im Exposuremanagement-Tab vom Unified Secops Portal werden schon im vorhinein priorisierte **Konfigurationsvorschläge** inkl. deren **Risiko-Score** zu einzelnen Endpunkten / Plattformen gezeigt. 
Derzeit zieht das Exposuremanagement Daten aus folgenden Quellen:
- Microsoft Defender für Endpunkt
- Microsoft Defender for Identity
- Microsoft Defender for Cloud Apps
- Microsoft Defender für Office
- Microsoft Defender für IoT
- Microsoft-Sicherheitsbewertung
- Microsoft Defender Sicherheitsrisikomanagement
- Microsoft Defender für Cloud
- Microsoft Entra-ID
- Microsoft Defender External Attack Surface Management (EASM)
