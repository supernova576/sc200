## Beschreibung
RESTful Endpoint für viele Microsoft Dienste. Man benötigt eine App Registration, um auf diese Daten zuzugreifen. Graph korreliert die Daten und bereitet sie auf. 
> Endpoint: graph.microsoft.com
## Kerninhalte
- **Microsoft 365-Kerndienste:** Bookings, Kalender, Delve, Excel, Microsoft Purview-eDiscovery, Microsoft Search, OneDrive, OneNote, Outlook/Exchange, Personen (Outlook-Kontakte), Planner, SharePoint, Teams, To Do, Viva Insights
- **Enterprise Mobility + Security Dienste:** Advanced Threat Analytics, Advanced Threat Protection, Microsoft Entra, Identity Manager und Intune. 
- **Windows-Dienste:** Aktivitäten, Geräte, Benachrichtigungen, Universelles Drucken
- **Dynamics 365 Business Central-Dienste**
- **Microsoft Partner Center-Dienste**
## Missbrauch von Angreifern
Die Graph-API von Microsoft wird oft durch Angreifer missbraucht. Diese senden via [[(Spear-)Phishing]] einen Link für eine "Device-Activation", welche der Angreifer zuvor generiert hatte. Falls der Code für die Device-Activation eingegeben wird, können die Angreifer nun einen "offiziellen" Account für allgegenwertige Dinge nutzen (Filedownload, [[BEC|Emails versenden]]).
![[ms_graph_attack_beispiel.png]]



