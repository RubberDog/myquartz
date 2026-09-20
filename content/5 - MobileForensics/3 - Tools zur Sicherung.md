#### ElcomSoft iOS Forensic Toolkit

Elcomsoft bietet - für 2199€ - die Vollversion des Elcomsoft iOS Forensic Toolkit (EIFT) an.\
Es kann logical-, FFS- und Physical-Sicherungen durchführen.\
Beim EIFT handelt es sich - laut Script - um ein CMD-Tool. Empfohlen wird der automatisch Flow, der manuelle Flow sollte nur von erfahrenen Usern gewählt werden.\
Am Beispiel eines iPhone4 werden die folgenden Schritte einer Sicherung beschrieben:\
- DFU-Mode aktivieren
- Laden der RAMDisk des Toolkit
- Bruteforce des Gerätesperrcodes
- Extrahieren der Keys, um Daten und Keychain zu entschlüsseln
- Entschlüsseln der Keychain
- Imageerstellung
- Entschlüsseln der Daten und bilden eines SHA1-Hashes

Zwar ist das EIFT schnell in der Sicherung, für die Aufbereitung der Daten wird allerdings ein weiteres Tool benötigt, dazu ist der EIFT nicht in der Lage.

Anhand von Screenshots wird der Sicherungsprozess erklärt, wirklich unwichtig für uns..

#### Cellebrite UFED Physical Analyzer

Mit dem UFED (Universal Forensic Extraction Device) PA (Physical Analyzer) können iOS-Geräte ausgelesen und aufbereitet werden.\
Hierbei wird FFS- und Physical-Sicherung unterstützt, wobei FFS hier "advanced logical acquisition" genannt wird.\
Der PA kann die erhaltenen Daten auch direkt aufbereiten.

Anhand von Screenshots wird der Sicherungsprozess erklärt, wirklich unwichtig für uns..

#### Magnet Axiom

Axiom untersützt grundsätzlich die logical- und FFS-Sicherung für iOS-Geräte.\
Bereits während der Sicherung können die schon ausgelesenen Daten betrachtet werden, was ggf. Zeit spart.

Anhand von Screenshots wird der Sicherungsprozess erklärt, wirklich unwichtig für uns..

#### Oxygen Forensic Detective

Oxygen Forensic Detective unterstützt logical-, FFS- und Physical-Sicherungen.\
Der integrierte SQLite- wie auch PList-Viewer sind für die Aufbereitung von Smartphone-Sicherungen essentiell.\
Zusätzlich kann es gelöschte SQLite-Einträge wiederherstellen und Cloud-Daten analysieren.

Anhand von Screenshots wird der Sicherungsprozess erklärt, wirklich unwichtig für uns..


#### Open Source Analyse

Egal was das Skript sagt, Empfehlung für Sicherungen bei bekanntem Sperrcode ist klar [UFADE](https://github.com/prosch88/UFADE) von [Christian Peter](https://it-forensik.fiw.hs-wismar.de/index.php?title=Christian_Peter_(MT)) (Master-Arbeit an der WINGS)