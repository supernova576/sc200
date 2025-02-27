## Beschreibung
Die Threat Intelligence Platform ist eine digitale Sandbox, die Files systematisch nach Malware oder anderen schädlichen Files abscannt. Dieses Modul ist auf folgenden Seiten ersichtlich: 
- [[Defender XDR]]
- [[Azure Sentinel]]
- [[Unified Security Portal]]

## Threat Intelligence Module
![[ti_sentinel.png]]

| Reiter  | Beschreibung                                                                                  |
| ------- | --------------------------------------------------------------------------------------------- |
| Add new | Manuelles Hinzufügen von: <br>- TI Object (Indicator, Identity, Threat Actor, Attack Pattern) |
| Import  | Importieren von IOCs durch:<br>- File (CSV/JSON)<br>- Connector (im Content hub installieren) |
Der Import von einer IP-Adress-Range ist am schnellsten, wenn man ein CSV-File mit den jeweiligen IP-Adressen erstellt und anschliessend hochlädt.

