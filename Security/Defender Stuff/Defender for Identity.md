## Beschreibung
Defender for Identity ist eine hybride Securitylösung (Daten von on-prem AD und Cloud AD), um Identitäten besser zu schützen. Mit Defender for Identity kann man beispielsweise nicht nur Daten für Alerts enrichen, sondern auch **identitätsbasierte** Attacken (bsp. gehackte Accounts) durch UEBA ([[Defender XDR#UEBA Policies]]) erkennen und alarmieren.
Monitort auch Änderungen von Gruppen in Form von Audit-Logs.
## Konfiguration

#### Sensitive Accounts (Entity Tags)
Sensitive Accounts müssen separat als "sensitiv entity" getaggt werden. Folgende Optionen stehen als Taggingoptionen zur Verfügung
1. Sensitive Account (verbietet "insecure Kerberos delegation")
2. Honeytoken Accounts (siehe [[Honeypots (-tokens)]]), gilt für **Benutzer** und **Devices**!
3. Exchange Server
Es wird als best Practice angesehen, dass man einen oder sogar mehrere Honeytoken Accounts erstellt, welche einen Alert Triggern wenn versucht wird, sich dort anzumelden.
##### Accounts für Attacker
Wenn man extra einen Account für Angreifer erstellt, dann hilft nur der **Honeytoken**-Entity-Tag. Accounts / Devices, welche den Sensitive-Entity-Tag haben, alarmieren **nicht**!
