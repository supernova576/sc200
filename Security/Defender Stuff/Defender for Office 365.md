## Beschreibung
Defender für Office365 spezialisiert sich auf Email-Verkehr (Outlook). Es analysiert Anhänge von Mails (bsp. Word, Excel, usw.) und kontrolliert diese auf Malware. Braucht keinen Agent, da er direkt auf dem Server läuft.

## SecOps Mailbox
Eine SecOps Mailbox ist eine Mailbox für Security Analysten, welche sich ALLE Mails anschauen müssen. Somit ziehen Filter bei einer solchen Mailbox **nicht**, und alle Mails werden durchgelassen.

## wichtige Features
#### Safe Attachments
Safe Attachments ist ein Feature, welches Attachments (z.B. von einem Mail) zuerst in eine Sandbox ([[Threat Intelligence Platform]]) schickt, welche dieses auf Malware analysiert. Es gibt mehrere Varianten, wie Safe Attachments funktionieren kann:
###### Off
Mit dieser Konfiguration ist das Feature **deaktiviert**.
###### Monitor
Das Attachment wird zuerst gescannt und erst dann wird das **ganze Mail** gesendet. 
Blockiert detektierte Malware nicht, sondern loggt nur, wohin diese geht (Empfänger). Gut für Simulationen, ansonsten sehr gefährlich.
###### Block
Das Attachment wird zuerst gescannt und erst dann wird das ganze Mail gesendet. Blockiert detektierte Malware und sendet das ganze Mail in die Quarantäne. **Künftige Mail**s mit dem gleichen Attachment werden automatisch blockiert und in die Quarantäne gesendet.
###### Dynamic Delivery
Durch Dynamic Delivery wird das Mail sofort an den Empfänger gesendet (reduziert Wartezeit). Das Attachment wird jedoch durch einen Platzhalter ersetzt (heisst Attachment ist nicht das Originale), bis die Sandbox fertig ist mit der Analyse. Anschliessend wird das Attachment (falls nicht malicious) an den Benutzer gesendet.
#### Attack Simulation
Um die Awarness von Benutzern zu trainieren, offeriert Defender for Office 365 ein Attack Simulation Training, welches vollautomatisch Kampanien starten kann. In der Attack Simulation Übersicht sieht man, welche Kampanien ongoing sind und wie viele Personen auf die Attack Simulation hereingefallen sind.
###### Typen von Attack Simulation
- Credential Harvest => normales Phishing
- Malware Attachment => Custom Attachment als Payload
- Link in Attachment 
- Link to Malware
- Drive-by URL
- OAuth Consent Grant
- How-to Guide
###### Trainings aufgrund von Attack Simulation
DFO365 bietet die Möglichkeit, Benutzern welche auf den Link geklickt haben, direkt in eine Schulung zu senden.
## Fragen und Knowledge Check (Kapitelprüfung)

| Q                                                | A                                                                                               |
| ------------------------------------------------ | ----------------------------------------------------------------------------------------------- |
| Braucht Defender for Office einen Agent?         | Nein. Defender for Office braucht **keinen** Agent                                              |
| Was sind "Safe Attachments"? Wie ist der Ablauf? | Mails und Attachments werden zu einer Sandbox gesendet, wo die Files separat analysiert werden. |
| Welches Szenario ist keine Attack Simulation?    | Bitcoin Mining                                                                                  |
