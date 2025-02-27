## Usecases

#### Sentinel Alert Rule Änderungen auslesen
Um zum Beispiel zu schauen, ob Änderungen an Alerts vorgenommen wurden.
``` kql
SentinelAudit
| where OperationName == "Microsoft.SecurityInsights/alertRules/write"
```

![[Azure Sentinel#Advanced Hunting Query]]

## Parsers
#### ASIM Parser
Der ASIM Parser normalisiert eingehende Daten in ein entprechendes Format.
> Wichtig! Der ASIM Parser updated von **alleine**.

Alle wichtigen ASIM Data Tables und wie man diese abfragen kann, können [hier](https://learn.microsoft.com/en-us/azure/sentinel/normalization-about-schemas) gefunden werden. 
#### Custom Parser (unifying Parser)
Um den automatischen Updates des ASIM-Parsers aus dem Weg zu gehen, kann man einen eigenen Parser deployen. Wichtig beim Deployen ist, dass man **CallerContext** auf Any und **SourceSpecificParser** auch auf Any setzt.
Weiterhin sollten Analytics Rules, welche den neuen Parser verwenden **keine** Zeitangaben haben.
###### Field Extraction
Felder, welche durch einen Custom-Parser extrahiert werden sollten, können entweder mit REGEX oder mit dem "[[KQL (Syntax)#parse|parse]]" Command (KQL) extrahiert werden.
##### Generelle Best Practices Advanced Hunting Queries
Immer **ReportId** und **DeviceId** mitgeben (falls im Table vorhanden). Somit gelingt es einfacher, Daten mit einem Join zu enrichen.

## Syntax
#### Basic Search Syntax
###### Where
Sucht nach Daten innerhalb eines Fields.
```kql
SecurityEvent | 
where EventID == 4334
```
###### Search
Search sucht wie where nach Keywords. Hier muss man kein Field angeben, da **search** über alle Fields sucht.
```kql
search "err"

OR

search in (SecurityEvent, SecurityAlert) "err"
```
#### Data Projection
###### Project
Zeigt Daten aus einem Field an.
```kql
SecurityEvent | 
project EventID
```
###### distinct / summarize
Wie stats cd(row) in Splunk. Fasst alle Ergebnisse zusammen.
```kql
SecurityEvent | 
distinct EventID

OR

SecurityEvent |
extend count = summarize count() by Account |
project count
```
###### Render
Um Datenvisualisierungen zu machen, kann der **render** Command benutzt werden. Folgende Charts können erstellt werden:
- areachart
- barchart
- columnchart
- piechart
- scatterchart
- timechart
```kql
SecurityEvent | 
summarize count() by Account | 
render barchart
```
#### Data Extension
###### Let
Mittels Let kann man eine zusätzliche Variable definieren. Dies kann als einfache Variable oder Liste geschehen.
```kql
let timeOffset = 7d; 
let discardEventId = 4688; 
SecurityEvent | 
where TimeGenerated > ago(timeOffset*2) and TimeGenerated < ago(timeOffset) | 
where EventID != discardEventId

OR 

let suspiciousAccounts = datatable(account: string) [ @"\administrator", @"NT AUTHORITY\SYSTEM" ]; SecurityEvent | 
where Account in (suspiciousAccounts)
```
###### Extend
Wie **let**, jedoch können mit Extend auch kalkulierbare Ergebnisse gespeichert werden.
```kql
SecurityEvent | 
where ProcessName != "" and Process != "" | 
extend StartDir = substring(ProcessName,0, string_size(ProcessName)-string_size(Process))
```
#### Table Joins
###### Join
Funktioniert wie ein regulärer Join. Es gibt mehrere Optionen, wie man die Daten joinen möchte (inner, left, outer, right, ...). Wird meistens für eine andere Table verwendet, um gewisse cols auszulesen.
```kql
SecurityEvent | 
where EventID == "4624" | 
summarize LogOnCount=count() by EventID, Account | 
project LogOnCount, Account | 
join kind = inner ( 
	SecurityEvent | 
	where EventID == "4634" | 
	summarize LogOffCount=count() by EventID, Account 
	| project LogOffCount, Account 
) on Account
```

###### Union
Der Union Command gibt **ALLE** Daten eines (oder mehreren) anderen Tables mit. Nützlich, wenn man über mehrere Tables gleichzeitig sucht.
```kql
SecurityEvent | 
union SigninLogs
```

## Data Parsing

#### parse
```kql

let Traces=datatable(EventText: string)
    [
    "Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=23, lockTime=02/17/2016 08:40:01, releaseTime=02/17/2016 08:40:01, previousLockTime=02/17/2016 08:39:01)",
    "Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=15, lockTime=02/17/2016 08:40:00, releaseTime=02/17/2016 08:40:00, previousLockTime=02/17/2016 08:39:00)",
    "Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=20, lockTime=02/17/2016 08:40:01, releaseTime=02/17/2016 08:40:01, previousLockTime=02/17/2016 08:39:01)",
    "Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=22, lockTime=02/17/2016 08:41:01, releaseTime=02/17/2016 08:41:00, previousLockTime=02/17/2016 08:40:01)",
    "Event: NotifySliceRelease (resourceName=PipelineScheduler, totalSlices=27, sliceNumber=16, lockTime=02/17/2016 08:41:00, releaseTime=02/17/2016 08:41:00, previousLockTime=02/17/2016 08:40:00)"
];

Traces  
| parse kind=regex EventText with "(.*?)[a-zA-Z]*=" resourceName @", totalSlices=\s*\d+\s*.*?sliceNumber=" sliceNumber: long  ".*?(previous)?lockTime=" lockTime ".*?releaseTime=" releaseTime ".*?previousLockTime=" previousLockTime: date "\\)"  
| project resourceName, sliceNumber, lockTime, releaseTime, previousLockTime
```