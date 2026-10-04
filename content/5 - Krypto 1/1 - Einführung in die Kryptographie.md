Die Sicherheit eines kryptographischen Verfahrens liegt nicht darin, einen möglichst komplexen Weg zur Schlüsselerzeugung zu finden und diesen geheim zu halten, sondern die Anzahl möglicher Schlüssel so hoch zu halten, dass die pure Menge nicht mehr in realistischer Zeit durchprobiert werden kann.


Kryptographische Anwendungen lassen sich grob in drei Kategorien unterteilen:

- symmetrische Verschlüsselungen
- asymmetrische Verschlüsselungen
- Protokolle

Kryptographische Systeme beinhalten immer Funktionen, die mittels Schlüssel auf Nachrichten oder Schlüsseltexte angewendet werden.

Wichtig ist hierbei, dass das Ergebnis immer eindeutig ist - kein Element eines Geheimtextes darf die Abbildung verschiedener Elemente des Klartextes sein (-> Bijektivität).

Der Klartext `x` wird auf dem Geheimtext `y` eindeutig abgebildet, und die inverse Funktion, also die Entschlüsselung, ergibt dann wieder den Klartext `x`. Ohne eine Eindeutigkeit könnte der Empfänger nicht feststellen, welche Nachricht der Sender geschickt hat.

Kryptographische Systeme lassen sich nach Einsatzzweck und Schlüsselverwaltung klassifizieren;
- Systeme zur Geheimhaltung von Nachrichten
- Systeme die Nachrichten vor unbemerkter Veränderung schützen

Systeme zur Geheimhaltung von Nachrichten haben das Schutzziel der Vertraulichkeit.\
Systeme zum Schutz vor unbemerkter Veränderung sind Authentifikationssysteme, welche das Schutzziel der Integrität verfolgen.

Die Klassifizierung anhand der Schlüsselverteilung ist unterteilt in symmetrische und asymmetrische Systeme.

Historische Verfahren sind symmetrisch, d.h. Sender und Empfänger benötigen den gleichen Schlüssel für Ver- und Entschlüsselung.

In den 1970er Jahren wurden asymmetrische Verfahren der Kryptographie erfunden. Hierbei wird ein Schlüsselpaar benutzt; ein öffentlicher und ein privater Schlüssel.\
Zum Verschlüsseln von Nachrichten benutzt der Sender den öffentlichen Schlüssel des Empfängers, nur mittels des privaten Schlüssels kann die Nachricht entschlüsselt werden.\
Der größte Vorteil hierbei ist, dass kein geheimer Schlüssel ausgetauscht werden muss, es muss lediglich sichergestellt werden, dass der öffentliche Schlüssel auch wirklich dem gewünschten Empfänger gehört.

Durch asymmetrische Verfahren ist auch die digitale Signatur möglich: Die unterschreibende Person nutzt ihren privaten Schlüssel zum signieren einer Nachricht, und jeder kann mittels der zugehörigen, öffentlichen Schlüssels die Echtheit der Nachricht verifizieren.

Das Intuitive Ziel kryptographischer Verfahren ist die Vertraulichkeit, so dass nur ein bestimmter Adressat die Nachricht lesen kann.

Weitere Aspekte sind Authentizität, Integrität, Anonymität und Verbindlichkeit.

Abbildung aus dem Script:\
![[Pasted image 20261004110209.png]]


#### 1.2 Einordnung der Kryptographie

Kryptographie wird häufig in öffentlichen Netzen, z.B. dem Internet genutzt.\
Sie löst jedoch nur eines der Probleme, die im öffentlichen Raum entstehen - nämlich das der Vertraulichkeit.\
Der Empfänger einer Nachricht muss jedoch auch sichergehen können, dass diese Nachricht tatsächlich vom genannten Absender kommt (Authentizität), als auch dass die Nachricht nicht manipuliert wurde (Integrität).

Zur Verschlüsselung von Inhalten wird üblicherweise auf symmetrische Verschlüsselung zurückgegriffen, da diese wesentlich effizienter ist als die asymmetrische Verschlüsselung.\
Ein großer Nachteil ist jedoch, dass hierfür der Schlüsselaustausch stattfinden muss, welcher mit einer asymmetrischen Verschlüsselung umgangen werden kann.

Asymmetrische Kryptographie beruht wesentlich auf der angenommenen Schwierigkeit bestimmter mathematischer Probleme, z.B. dem Problem eine natürliche Zahl in ihre Primfaktoren zu zerlegen oder das sogenannte "Diskrete Logarithmus-Problem".\
Aus diesen mathematischen Problemen lassen sich Einwegfunktionen ableiten, welche leicht zu berechnen aber schwer umzukehren sind.

Auf Basis des "Diskrete Logarithmus-Problems" lassen sich z.B. Verfahren zum Schlüsselaustausch konstruieren.\
In den letzten Jahrzehnten wurden zahlreiche kryptographische Verfahren entwickelt, beispielsweise:
- Block- und Stromchiffre zur Verschlüsselung
- Verfahren zum Schlüsselaustausch
- Verfahren zur Erstellung digitaler Signaturen
- Hashfunktionen
- Pseudozufallszahlengeneratoren

Diese Verfahren werden in IT-Sicherheitsprodukten zur Absicherung von Kommunikation als Teil von Protokollen wie Transport Layer Security (TLS) oder Internet Protocoll Security (IPsec) genutzt.\
IPsec erweitert das IP-Protokoll zum Versand von Datenpaketen über das Internet um eine Möglichkeit zur Verschlüsselung und Authentisierung.

Ein VPN wird in der Regel mittels IPsec umgesetzt, es gibt aber auch Lösungen unter Verwendung von TLS, z.B. OpenVPN.

Zur Schlüsselaushandlung nutzt IPsec üblicherweise das Internet Key Exchange (IKE) Protokoll.\
Hierbei wird mittels asymmetrischem Schlüsselaustausch ein gemeinsames Geheimnis ausgehandelt, aus dem die symmetrischen Session-Keys für IPsec abgeleitet werden.

Abbildung 4 aus dem Script:\
![[Pasted image 20261004125010.png]]

Steganographie ist verborgene Speicherung oder Übermittlung von Informationen in einem Trägermedium, der Einsatz hat Geheimhaltung und Vertraulichkeit zum Ziel.

Bei der Transposition werden die Zeichen eines Klartextes umsortiert (Permutation).\
Substitution lässt die Zeichen an ihrem Platz, ersetzt sie jedoch durch andere (Caesar-Chiffre).


#### 1.3 Ziele des Einsatzes kryptographischer Verfahren

Eine weit verbreitete Möglichkeit zur Realisierung des Schlüsselaustausches bei symmetrischen Verfahren stellt der Ansatz nach Diffie und Hellmann dar.

Abbildung symmetrischer Verschlüsselung:\
![[Pasted image 20261004125934.png]]

und asymmetrische Verschlüsselung:\
![[Pasted image 20261004125958.png]]

Darüber hinaus sind Authentizität und Integrität äußerst wichtig bei kryptographischen Verfahren\
Authentizität soll dem Empfänger garantieren, dass die Nachricht auch wirklich von dem stammt, der sich als Absender ausweist, und Integrität soll gewährleisten dass die Nachricht nicht verändert wurde.

Verbindlichkeit als weiterer Faktor bedeutet, dass auch gegenüber dritten eindeutig nachgewiesen werden kann, wer Autor einer Nachricht war.