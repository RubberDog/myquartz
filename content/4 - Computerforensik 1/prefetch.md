
Suche mittels `fls -pr /dev/loop0p2 | grep -i prefetch`

Alle passenden Dateien finden sich im Ordner `Windows\prefetch`

Empfehlung wäre, logisch mittels `cp` alle Dateien im Prefetch-Ordner herauszukopieren, statt dies einzeln via z.B. [[icat]] zu machen.

Windows lädt vorab Teile von Programmen (DLLs, Dynamic Link Libraries) um häufig genutzte Programme schneller starten zu können.