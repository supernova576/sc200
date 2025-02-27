## Beschreibung
Spezialisiert sich auf die Sicherheit der **Infrastruktur** der Cloud (Azure). Ist auch im [[Defender XDR]]-Portal zu sehen.

## Security Recommendations
#### Prevent future alerts
Gibt Schritte und Empfehlungen an, die beschriebene Art von Attacken für **künftige** Alerts zu verhindern
#### Mitigate the threat
Gibt Schritte und Empfehlungen an, die beschriebene Art von Attacken **für diesen Case** zu lösen.
#### Workload Protection
Anbei ein Bild der Übersicht vom Workload Protection Dashboard. Dieses Dashboard bietet eine Übersicht über alle verwalteten Assets. Das Dashboard gibt auch "Security Recommendations" ab.
![[worklaod protection defender for cloud.png]]

## Submodules
Die folgenden Sub-Modules sind [hier](https://learn.microsoft.com/en-gb/training/modules/understand-azure-defender-cloud-workload-protection/) ausführlicher dokumentiert. Folgende Kapitel sind zusammengefasst.
#### Defender for Key Vault
###### Beschreibung
Defender for Keyvault schaut, ob ein Secret (Key) auf maliziöse Art und Weise gebraucht oder ausgelesen wird.
###### Usecases
Folgende Usecases sind die Gängigsten:
- Access from sus IP (Zugriff bereits erfolgt)
- Access from [[TOR#Architektur|TOR exit Node]]
- High volume of operations in Key Vault
- Sus policy change incl. sus query/read of secret
- Unusual Access / too many denies on secret

#### Defender for Servers
###### Beschreibung
Bietet erweiterte Sicherheit für Linux oder Windows Server, egal ob on-prem, in Azure oder sogar in AWS. Die Verbindung zu Sentinel bzw. Azure erfolgt über [[Azure Arc]].
###### Usecases (Plan 1&2)
Generell unterscheidet man zwischen Plan 1 und Plan 2. Plan 1 enthält alle "Basicfunktionen", wie beispielsweise:
- Vuln Management (ähnlich wie [[Defender for Endpoint#Vulnerability Scanning]])
- Deployment von überall
- Integration für MDE und Microsoft Defender for Cloud
**Plan 2** hingegen offeriert noch viele weitere Features wie beispielsweise:
- Just in Time Access (Live Session) zum Server
- Log Analytics (500 MB free)
- Threat Detections: OS Level und Netzwerk Layer
- File Integrity Monitoring
Alle Benefits und der Vergleich können [hier](https://learn.microsoft.com/en-gb/training/modules/understand-azure-defender-cloud-workload-protection/2-understand-azure-defender-for-servers) gefunden werden.

#### Defender for App Service
###### Beschreibung
Defender for App Service spezialisiert sich auf das Monitoring von Web-Apps sowie [[API]]. Falls man bereits einen windowsbasierten Service Plan benutzt, werden auch VMs oder Sandboxen mitgescannt.
###### Usecases
Alarmiert bei Directory-Blasting oder anderen Schwachstellenproben. Defender for App Service gibt Security Recommendations und Alerts zurück.

#### Defender for Storage
###### Beschreibung
Triggert Alerts wenn jemand versucht, sich maliziös Zugriff zum Storage zu verpassen. Basiert auf anomaly detection.
###### Übersicht
![[defender-for-storage-overview.png]]
###### Usecases
| Usecase                      | Beschreibung                                                                                                            |
| ---------------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| Unusual Access Pattern       | Bsp. erfolgreiches Connecten via TOR oder IPs, welche als sus von der [[Threat Intelligence Platform]] geflaggt werden. |
| Sus Activities               | Unusual change of Perms                                                                                                 |
| Upload von malicious Content | Wenn Malware auf dem Storage gefunden wird.                                                                             |
#### Defender for SQL
###### Beschreibung
Schützt eine SQL Datenbank, indem [[Syntax (SQL)|SQL-Queries]] gemonitort werden (bsp. SQL Injection oä.). Auch werden mit Defender for SQL Datenbanken auf allfällige Vulnerabilities gescannt. Auch maliziöse Verbindungen und Logins werden alarmiert
###### Scope
Dieser Defender richtet sich nur an:
- Azure SQL
- SQL Server auf Maschinen
- Azure Cosmos DB
###### Übersicht
![[defender-alerts-for-sql.png]]

#### Defender for open-source Databases
###### Beschreibung und Scope
Genau gleiches Prinzip wie Defender for SQL, jedoch sind hier folgende Datenbanken im Scope:
- [[MySQL]]
- MariaDB
- Postgresql

#### Defender for Ressouce Manager
###### Beschreibung
Defender for Ressource Manager macht eigentlich genau das, was der Name bereits verrät. Er schaut sich die Ressourcen an.
###### Usecases
| Usecase                            | Beschreibung                                                                 |
| ---------------------------------- | ---------------------------------------------------------------------------- |
| Sus Ressouce Management Operations | Operations von sus IPs, Scripts oder das Ausschalten von Antimalware Engines |
| Use of exploit Toolkits            | ZB. Microburst oder PowerZure                                                |
| Lateral Movement                   | Vom Azure Management Layer zum Ressource Layer                               |

#### Defender for DNS
###### Beschreibung
Monitort jeglichen [[DNS|DNS-Traffic]] auf sus Aktivitäten. Kann Alerts generieren, wenn zum Beispiel ein DNS-Eintrag als IOC in der [[Threat Intelligence Platform]] vorliegt.
Auch Usecases wie [[DNS-Tunneling]] sind mit dem Defender for DNS abgedeckt.

#### Defender for Containers
###### Beschreibung
Die Cloud-Native Lösung zum Schützen von Containern innerhalb einer VM/Clusters.
###### Scope
Defender for Containers berücksichtigt folgende Container:
- Azure Kubernetes Service
- Amazon Elastic Kubernetes Service
- Jegliche unmanaged Kubernetes Services (Verbindung mit [[Azure Arc]])
###### Usecases
- Environment hardening (Sicherheits - Konfigurationsparameter tunen)
- Vuln Assessment (Scanning auf Schwachstellen)
- Realtime Threat Protection
