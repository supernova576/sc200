## Rollen
#### Sentinelspezifische Rollen

| Rolle                      | Nutzen                                                                                                                    |
| -------------------------- | ------------------------------------------------------------------------------------------------------------------------- |
| Sentinel Reader            | Incidents und Workbooks sehen                                                                                             |
| Sentinel Responder         | **Sentinel Reader** +<br>Incidents managen (Status updaten, (User-)Assignments machen)                                    |
| Sentinel Contributor       | **Sentinel Responder** + <br>Analytics Rules und Workbooks erstellen/verwalten, Installationen vom Contenthub durchführen |
| Logic App Contributor      | **Sentinel Playbook Operator** +<br>Kreieren von Editieren von Playbooks                                                  |
| Sentinel Playbook Operator | Playbooks sehen und laufen lassen.                                                                                        |
#### Azure EntraID spezifische Rollen

| Rolle                  | Nutzen                                                                                     |
| ---------------------- | ------------------------------------------------------------------------------------------ |
| Security Operator      | **Security Reader** +<br>Kann Security Events kreieren und verwalten                       |
| Security Reader        | Kann Security Events und dazugehörige Daten (EntraID, ...) lesen                           |
| Security Administrator | **Security Operator + Reader** +<br>Kann applikationsspezifische Konfigurationen verwalten |
#### Copilot for Security Rollen
| Rolle               | Nutzen                                                                                                                                                                         |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Copilot Contributor | Kann Promptbooks erstellen/laufen lassen und Prompts kreieren und laufen lassen. <br>Kann auch Files hochladen.<br>Alles was man benötigt, um Copilot **gebrauchen** zu können |
| Copilot Owner       | Alles was man benötigt, um Copilot **gebrauchen und konfigurieren** zu können.                                                                                                 |
## RBAC
RBAC steht für Role-Based Access Controll. RBAC-Rollen sind im Grunde genommen nichts anderes als eine Gruppierung von Azure-Rollen, welche einer Ressource oder einem Benutzer zugewiesen werden können.
#### RBAC auf Log-Analytics-Table Ebene
RBAC Rollen können auch auf einzelne Tables in einem [[Log Analytics Workspace]] angewendet werden.