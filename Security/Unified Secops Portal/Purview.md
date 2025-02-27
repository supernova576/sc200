## Beschreibung
Modul für das Verhindern von Insider Risks ([[DLP|Datenabfluss]]). Suchen von Daten ist über Purview auch möglich.

## Insider Risk Management Policy
Die Insider Risk Management Policy dient dazu, dass Datenleaks durch ein [[DLP]]-System (Purview) abgefangen werden. Die Insider Risk Management Policy nutzt (wie in der Abbildung unten zu sehen ist) auch [[Defender XDR#UEBA Policies|UEBA]], um nach potenziellen DLP-Cases zu filtern.
![[insider risk policy alert generation.png]]

## Unterschiede Standard und Premium

#### Standard
- Enabled by default,
- audit events search,
- compliance portal,
- search unifiedauditlog cmdlet,
- export csv,
- office 365 management activity,
- 180 day log retention,
- benötigt nur "basic"-Subscriptions
#### Premium
Alles was standard hat +
- 1-year log Data retention,
- 10-year log retention,
- audit log retention policies,
- intelligent insights,
- benötigt high-tier subscriptions (teurer als normal)

## Exportieren von Dateien
Das Exportieren von Daten ist als CSV möglich. Dabei sind die eigentlichen Daten im CSV-Format.

## Suchen via Purview
Purview bietet drei verschiedene Suchkategorien. [Purview Portal](https://purview.microsoft.com)
![[purview_teams_search_1.png]]
Beispielsweise kann über die Location **Exchange Mailboxes** Teams-Content ausgelesen werden.
Weiterhin wird anschliessend zwischen drei **types** unterschieden, um die eigentlichen Daten zu suchen:

| Typ       | Beschreibung                                                                                                                   |
| --------- | ------------------------------------------------------------------------------------------------------------------------------ |
| Category  | Kategorien, welche Benutzer eigens erstellt haben. Hier muss man nach Farbe suchen (Bsp. Category: Remote => Suchfeld: yellow) |
| ItemClass | Spezifische third-party data types, welche zuvor importiert wurden.                                                            |
| Kind      | Typ von der zu suchenden Nachricht (bsp. microsoftteams oder meetings oder contacts, ...)                                      |
## Kapitelfragen
1. welches feature ist bei beiden Varianten gleich? => cmdlet (multiple choice),
2. wie sind die unterschiede zwischen audit standard und audit premium lizenzen? => premium benötigt higher-tier subscriptions,
3. Wie viele Suchen können gleichzeitig laufen? => 10,
4. wie behandelt purview premium doppelte einträge? => by filtering out duplicates within an hour if certain properties do not change,
5. Wie viele Einträge (Zeilen) können auf einmal exportiert werden? => 50'000 Einträge,
6. Wie lange ist die längste retention zeit für purview premium? => 10 Jahre,
7. Was ist der Hauptunterschied zwischen Purview Standard und Premium => Audit (Standard) offers 180 Days log retention (Multiple Choice),
8. Welcher Schritt muss vor dem suchen nach audit logs gemacht werden? => confirm that audit log serach is enabled,
9. Welches feature von microsoft purview Premium ist essenziell um sensitive kommunikation sicher zu verwalten? => mailitemsAccessed,
10. Was ist der primäre Nutzen von exportieren CSVs? => To perform deteiled data analysis and meet compliance reporting requirements,
11. Wie werden audit einträge in purview Premium bei konflikten priorisiert? => by a priority level set by the administrator