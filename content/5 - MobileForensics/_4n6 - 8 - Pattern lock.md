
Den Part finde ich noch lustig, klappt aber nur bei wirklich alten Geräten, die unverschlüsselt sind.\
Ist ein Patternlock (als Display-Sperre) auf dem Gerät eingerichtet, helfen folgende Befehle - vorausgesetzt, TWRP ist installiert.

```shell
adb reboot recovery
adb shell
cd /data/system
rm -f .key
rm -f locksettings*
```

und nach nem reboot ins System ist das Patternlock weg.