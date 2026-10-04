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

Abbildung aus dem Script:
![[Pasted image 20261004110209.png]]

