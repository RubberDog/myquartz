### Anbindung eines Sniffers

#### Über einen Hub
In die mitzuschneidende Verbindung wird ein Hub integriert, welcher sämtlichen Traffic auf alle Ports leitet

Pro:
- einfache Handhabung
Con:
- kurze Unterbrechung im Netzwerk
- Sniffer ist für andere "sichtbar"
- Hubs werden kaum noch produziert
- GBit und schneller gar nicht existent

#### Über einen Switch via Mirrorport
Wenn der Switch über die Technik für einen Monitor- / Mirrorport verfügt, kann der Port des Sniffers so konfiguriert werden dass einer / eine Auswahl an / alle Ports dorthin gespiegelt werden

Pro:
- keine Änderungen an der Infrastruktur nötig
- keine Ausfälle oder Unterbrechungen durch die Einrichtung
Con:
- Paketverluste bei hohem Traffic

#### MitM
Ein klassischer MitM-Angriff, wenn kein Mirror verfügbar ist

Pro: 
- -
Con:
- ist ein Angriff (strafbar)
- keine Erfolgsgarantie
- side effects können den Netzwerktraffic stören, bis zum DoS
- unsauber, kontaminierter Traffic

#### Sniffer Inline
Der Sniffer wird direkt in die Verbindung integriert, so dass aller Traffic über ihn laufen muss.
Zwei Varianten: 
- Wird als IP-Device eingebunden, jedes IF erhält eine IP
	- Routing muss geändert werden
	- viel Konfigurationsaufwand in großen Netzen
- Wird als transparent Bridge eingebunden, keine IPs, keine Config-Änderungen nötig

Pro:
- - 
Con:
- kurze Unterbrechung
- Sniffer ist für andere "Sichtbar"

#### TAP-Device
Ein gesondertes Gerät wird eingebunden, verhält sich komplett transparent.

Pro:
- nicht Sichtbar im Netz
- kann nicht erreicht werden
Con: 
- kurze Unterbrechung beim Einbau
- Output für den Sniffer über 2 Ports, Gerät muss also über zwei Inputs (Netzwerkinterfaces) verfügen

| -                                        | Hub      | Mirror   | MitM              | Inline                        | TAP       |
| ---------------------------------------- | -------- | -------- | ----------------- | ----------------------------- | --------- |
| Sniffer erreichbar?                      | Ja       | Ja       | Ja                | Ja                            | Nein      |
| Aufzeichnung eventuell verschmutzt?      | Gering   | Gering   | Ja (!)            | Gering                        | Nein      |
| Unterbrechung der Kommunikation?         | Kurz     | Nein     | Ja (hohes Risiko) | Ja                            | Ja (kurz) |
| Administrative Maßnahmen erforderlich?   | Nein     | Ja       | Nein              | Ja / Nein (Je nach verfahren) | Nein      |
| Paketverluste?                           | Bei Last | Bei Last | Ja (hohes Risiko) | Gering                        | Gering    |
| Dauerhafte Störung des Betriebs möglich? | Nein     | Nein     | Ja (hohes Risiko) | Nein                          | Nein      |
